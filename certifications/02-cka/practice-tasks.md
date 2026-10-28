# CKA Practice Bank: 60 Hands-On Tasks

**Real exam:** 2 hours, about 15-20 performance-based tasks, pass mark about 66%. Docs at kubernetes.io are allowed.
**Domains (approx.):** Troubleshooting 30%, Cluster Architecture/Installation/Configuration 25%, Services & Networking 20%, Workloads & Scheduling 15%, Storage 10%.
This bank has 60 tasks so you can run three or four full timed sets (see Section "How to use"). Solutions are the commands and key YAML; adjust names, versions and namespaces to your lab.

## How to use
- **Set A:** tasks 1-20 (2 h). **Set B:** tasks 21-40. **Set C:** tasks 41-60. Or pick 15-18 mixed tasks across domains for a realistic set.
- Attempt each task before reading the solution. Verify with `k get` / `k describe`.
- Setup: `alias k=kubectl; export do="--dry-run=client -o yaml"; export now="--force --grace-period=0"`.

---

## A. Cluster Architecture, Installation & Configuration (Tasks 1-15)

**1.** Create a ClusterRole `node-reader` allowing get/list/watch on nodes, and bind it to user `jane`.
```
k create clusterrole node-reader --verb=get,list,watch --resource=nodes
k create clusterrolebinding node-reader-jane --clusterrole=node-reader --user=jane
k auth can-i list nodes --as=jane
```

**2.** In namespace `dev`, let ServiceAccount `ci` create and delete Deployments.
```
k -n dev create sa ci
k -n dev create role deploy-mgr --verb=create,delete --resource=deployments
k -n dev create rolebinding ci-deploy --role=deploy-mgr --serviceaccount=dev:ci
k -n dev auth can-i create deployments --as=system:serviceaccount:dev:ci
```

**3.** Upgrade the control plane node from v1.N to v1.N+1 using kubeadm.
```
k drain cp1 --ignore-daemonsets
apt-get update && apt-get install -y kubeadm=<ver>
kubeadm upgrade plan && kubeadm upgrade apply v<ver>
apt-get install -y kubelet=<ver> kubectl=<ver>
systemctl daemon-reload && systemctl restart kubelet
k uncordon cp1
```

**4.** Upgrade worker `node01` to the same version.
```
k drain node01 --ignore-daemonsets --delete-emptydir-data   # from control plane
# on node01:
apt-get install -y kubeadm=<ver> && kubeadm upgrade node
apt-get install -y kubelet=<ver> && systemctl daemon-reload && systemctl restart kubelet
k uncordon node01
```

**5.** Take an etcd snapshot to `/opt/etcd.db`.
```
ETCDCTL_API=3 etcdctl snapshot save /opt/etcd.db \
 --endpoints=https://127.0.0.1:2379 \
 --cacert=/etc/kubernetes/pki/etcd/ca.crt \
 --cert=/etc/kubernetes/pki/etcd/server.crt \
 --key=/etc/kubernetes/pki/etcd/server.key
```

**6.** Restore that snapshot into `/var/lib/etcd-restore` and make etcd use it.
```
etcdutl snapshot restore /opt/etcd.db --data-dir /var/lib/etcd-restore   # or etcdctl snapshot restore
# edit /etc/kubernetes/manifests/etcd.yaml: hostPath of volume etcd-data -> /var/lib/etcd-restore
# wait for etcd and API server to restart
```

**7.** Join a new worker to the cluster.
```
kubeadm token create --print-join-command      # on control plane
# run the printed kubeadm join ... on the new node
k get nodes
```

**8.** Drain `node01` for maintenance and bring it back.
```
k drain node01 --ignore-daemonsets --delete-emptydir-data
k uncordon node01
```

**9.** Check certificate expiry on the control plane and renew all.
```
kubeadm certs check-expiration
kubeadm certs renew all
# restart static pods (move manifests out and back, or restart kubelet)
```

**10.** Nodes are `NotReady` because no CNI is installed. Install a CNI.
```
k apply -f <cni-manifest.yaml>      # e.g. Calico/Flannel/Cilium per task instructions
k get nodes -w
```

**11.** Install an app from a Helm chart in namespace `tools`, overriding `replicaCount=3`.
```
helm repo add <name> <url> && helm repo update
helm install web <name>/<chart> -n tools --create-namespace --set replicaCount=3
helm list -n tools
```

**12.** Using Kustomize, build an overlay that sets replicas to 4.
```
# overlay/kustomization.yaml
resources: [../base]
patches:
- target: {kind: Deployment, name: web}
  patch: |-
    - op: replace
      path: /spec/replicas
      value: 4
k apply -k overlay
```

**13.** List CRDs and create an instance of an existing CRD kind `Backup`.
```
k get crd
k explain backup.spec
# write backup.yaml with apiVersion/kind from the CRD, then
k apply -f backup.yaml
```

**14.** Find the service cluster IP range and Pod CIDR configured in the cluster.
```
grep service-cluster-ip-range /etc/kubernetes/manifests/kube-apiserver.yaml
grep cluster-cidr /etc/kubernetes/manifests/kube-controller-manager.yaml
```

**15.** Create a user `dev1` certificate via CSR and grant it view access.
```
openssl genrsa -out dev1.key 2048
openssl req -new -key dev1.key -subj "/CN=dev1" -out dev1.csr
# create CertificateSigningRequest with base64 CSR, signerName kubernetes.io/kube-apiserver-client, usages [client auth]
k certificate approve dev1
k create clusterrolebinding dev1-view --clusterrole=view --user=dev1
```

---

## B. Workloads & Scheduling (Tasks 16-25)

**16.** Roll out `nginx:1.25` to Deployment `web`, then roll back.
```
k set image deploy/web nginx=nginx:1.25
k rollout status deploy/web
k rollout undo deploy/web
```

**17.** Scale Deployment `web` to 5 and create an HPA min 2, max 6, 70% CPU.
```
k scale deploy web --replicas=5
k autoscale deploy web --min=2 --max=6 --cpu-percent=70
```

**18.** Run a Pod using ConfigMap `app-config` as env vars and Secret `app-secret` as a volume at `/etc/secret`.
```
# pod spec: envFrom: [{configMapRef: {name: app-config}}]
# volumes: [{name: s, secret: {secretName: app-secret}}], volumeMounts: [{name: s, mountPath: /etc/secret}]
```

**19.** Label node `node01` with `disk=ssd` and schedule a Pod only there.
```
k label node node01 disk=ssd
# pod spec: nodeSelector: {disk: ssd}
```

**20.** Taint `node01` with `dedicated=gpu:NoSchedule` and run a Pod that tolerates it.
```
k taint nodes node01 dedicated=gpu:NoSchedule
# tolerations: [{key: dedicated, operator: Equal, value: gpu, effect: NoSchedule}]
```

**21.** Use node affinity so a Pod prefers zone `a` but may run elsewhere.
```
affinity:
  nodeAffinity:
    preferredDuringSchedulingIgnoredDuringExecution:
    - weight: 80
      preference:
        matchExpressions: [{key: zone, operator: In, values: [a]}]
```

**22.** Create a Pod with requests `cpu=100m,memory=128Mi` and limits `cpu=200m,memory=256Mi`.
```
k run r --image=nginx $do > p.yaml   # add resources block, then apply
```

**23.** Create a static Pod `static-web` on `node01`.
```
# on node01: grep staticPodPath /var/lib/kubelet/config.yaml
# place pod YAML (kind: Pod) in that directory; it appears as static-web-node01
```

**24.** Create a DaemonSet `logger` running on every node, including the control plane.
```
# DaemonSet with toleration: {key: node-role.kubernetes.io/control-plane, operator: Exists, effect: NoSchedule}
```

**25.** Create PriorityClass `high` (value 100000) and use it in a Pod.
```
k create priorityclass high --value=100000
# pod spec: priorityClassName: high
```

---

## C. Services & Networking (Tasks 26-37)

**26.** Expose Deployment `web` on port 80 as ClusterIP.
```
k expose deploy web --port=80 --target-port=8080
```

**27.** Expose `web` as NodePort 30080.
```
k expose deploy web --type=NodePort --port=80 $do > s.yaml
# set spec.ports[0].nodePort: 30080, then apply
```

**28.** Create an Ingress sending `/api` to Service `api:80` and `/` to `web:80`.
```
k create ingress main --rule="/api*=api:80" --rule="/*=web:80" --class=nginx
```

**29.** Route host `shop.example.com` to `shop:80` with Gateway API.
```
# HTTPRoute: parentRefs -> existing Gateway; hostnames [shop.example.com];
# rules: [{backendRefs: [{name: shop, port: 80}]}]
```

**30.** In namespace `prod`, allow ingress to Pods `app=db` only from `app=api` on TCP 3306.
```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata: {name: db-allow, namespace: prod}
spec:
  podSelector: {matchLabels: {app: db}}
  policyTypes: [Ingress]
  ingress:
  - from: [{podSelector: {matchLabels: {app: api}}}]
    ports: [{protocol: TCP, port: 3306}]
```

**31.** Apply a default-deny ingress policy to namespace `prod`.
```
spec: {podSelector: {}, policyTypes: [Ingress]}
```

**32.** Add a forwarder for `corp.local` to CoreDNS.
```
k -n kube-system edit cm coredns
# add: corp.local:53 { forward . 10.0.0.2 }
k -n kube-system rollout restart deploy coredns
```

**33.** Verify DNS resolution from inside a Pod.
```
k run t --image=busybox:1.36 --rm -it --restart=Never -- nslookup kubernetes.default
```

**34.** Find the CNI configuration and the Pod CIDR of `node01`.
```
ls /etc/cni/net.d/
k get node node01 -o jsonpath='{.spec.podCIDR}'
```

**35.** Create a headless Service for a StatefulSet `db`.
```
spec: {clusterIP: None, selector: {app: db}, ports: [{port: 5432}]}
# StatefulSet spec.serviceName must match the Service name
```

**36.** Service `shop` shows no endpoints. Fix it.
```
k get ep shop; k get svc shop -o yaml | grep -A3 selector
k get pods --show-labels
k label pod <pod> app=shop     # or fix the Service selector
```

**37.** Determine the kube-proxy mode in use.
```
k -n kube-system get cm kube-proxy -o yaml | grep mode
```

---

## D. Storage (Tasks 38-43)

**38.** Create a 1Gi hostPath PV, a matching PVC, and a Pod mounting it at `/data`.
```
# PV: capacity.storage 1Gi, accessModes [ReadWriteOnce], hostPath.path /mnt/data, storageClassName manual
# PVC: same class/size/mode; Pod volume persistentVolumeClaim.claimName
k get pv,pvc
```

**39.** Make StorageClass `fast` the default.
```
k patch sc fast -p '{"metadata":{"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'
```

**40.** Create a PVC that dynamically provisions from `fast`, and use it in a Pod.
```
# PVC: storageClassName: fast, requests.storage: 2Gi
```

**41.** Expand PVC `data` from 1Gi to 2Gi.
```
k patch sc <sc> -p '{"allowVolumeExpansion":true}'   # if not already
k patch pvc data -p '{"spec":{"resources":{"requests":{"storage":"2Gi"}}}}'
```

**42.** Change a PV's reclaim policy to Retain.
```
k patch pv <pv> -p '{"spec":{"persistentVolumeReclaimPolicy":"Retain"}}'
```

**43.** Run a Pod with a PVC using accessMode ReadWriteMany and two replicas sharing it.
```
# requires an RWX-capable backend; PVC accessModes [ReadWriteMany]; Deployment replicas: 2 using the same claim
```

---

## E. Troubleshooting (Tasks 44-60)

**44.** A node is `NotReady`. Fix it.
```
k describe node <n>
ssh <n>; systemctl status kubelet; journalctl -u kubelet -n 50
systemctl enable --now kubelet     # or fix config in /var/lib/kubelet/config.yaml
```

**45.** Kubelet fails because of a wrong CA path in its config.
```
grep -i ca /var/lib/kubelet/config.yaml /etc/kubernetes/kubelet.conf
# correct to /etc/kubernetes/pki/ca.crt, then systemctl restart kubelet
```

**46.** `kubectl` calls fail: API server is down.
```
crictl ps -a | grep apiserver; crictl logs <id>
# inspect /etc/kubernetes/manifests/kube-apiserver.yaml for typos in flags or paths
```

**47.** New Pods stay Pending with no events. Fix kube-scheduler.
```
k -n kube-system get pods | grep scheduler
# fix /etc/kubernetes/manifests/kube-scheduler.yaml (kubeconfig path or command typo)
```

**48.** Deployments do not create ReplicaSets. Fix controller-manager.
```
k -n kube-system describe pod kube-controller-manager-<node>
# fix flag/path in /etc/kubernetes/manifests/kube-controller-manager.yaml
```

**49.** etcd is crash-looping.
```
crictl logs <etcd-id>
# check data-dir, cert paths and --listen-client-urls in the etcd manifest
```

**50.** A Pod is Pending due to insufficient resources or a taint.
```
k describe pod <p>      # read Events: FailedScheduling
# lower requests, add toleration, or add capacity
```

**51.** A Pod is in CrashLoopBackOff.
```
k logs <p> --previous
k describe pod <p>
# fix command, config, or probes
```

**52.** A Pod is in ImagePullBackOff.
```
k describe pod <p>
k set image deploy/x c=<correct-image>
```

**53.** Service has no endpoints (selector vs labels, or Pods not Ready).
```
k get ep; k get pods --show-labels; k describe pod <p>
```

**54.** DNS fails inside Pods.
```
k -n kube-system get pods -l k8s-app=kube-dns
k -n kube-system logs deploy/coredns
k -n kube-system get cm coredns -o yaml
```

**55.** Ingress returns 503/404.
```
k describe ingress; k get ep <backend-svc>; k -n ingress-nginx logs deploy/ingress-nginx-controller
```

**56.** A PVC is stuck in Pending.
```
k describe pvc <p>      # no matching PV, class mismatch, or no default StorageClass
```

**57.** List cluster events sorted by time and save to a file.
```
k get events -A --sort-by=.metadata.creationTimestamp > /opt/events.txt
```

**58.** Find the Pod with highest CPU usage in namespace `default`.
```
k top pod -n default --sort-by=cpu | head -2
```

**59.** Get logs of container `sidecar` in Pod `app` and save them.
```
k logs app -c sidecar > /opt/sidecar.log
```

**60.** A rollout is stuck.
```
k rollout status deploy/web
k describe deploy web; k get rs; k describe pod <new-pod>
# causes: failing readiness probe, quota exceeded, bad image, unschedulable
k rollout undo deploy/web
```

---

## Self-review sheet
For each missed task: Task # | What failed | Correct approach | Doc page.
