# CKA Mock Exams

Use a real cluster (kubeadm on VMs, kind, or KodeKloud/killercoda labs). Time limit: 2 hours for 10 tasks is generous, so aim for 75 minutes to leave room for the full 15-20 task pace of the real exam.

## CKA Mock 1

| # | Weight | Task | Hints |
|---|--------|------|-------|
| 1 | 8% | A worker node shows `NotReady`. Find the cause and restore it. | `systemctl status kubelet`, `journalctl -u kubelet`, check kubelet config and certificates, `systemctl restart kubelet` |
| 2 | 8% | Upgrade the control plane node by one minor version with kubeadm. Drain first, uncordon after. | `kubeadm upgrade plan`, `apt-get install kubeadm=...`, `kubeadm upgrade apply`, upgrade kubelet/kubectl, `systemctl daemon-reload && restart kubelet` |
| 3 | 8% | Take an etcd snapshot to `/opt/etcd-backup.db`, then restore it to a new data directory and point the static pod at it. | `ETCDCTL_API=3 etcdctl snapshot save` with `--cacert --cert --key`, `snapshot restore --data-dir`, edit `/etc/kubernetes/manifests/etcd.yaml` hostPath |
| 4 | 5% | Create a 1Gi hostPath PV (RWO), a matching PVC, and a Pod mounting it at `/data`. | Match storageClassName, accessModes and size, verify `Bound` |
| 5 | 7% | In namespace `prod`, allow ingress to Pods `app=db` only from Pods `app=api` on TCP 3306. | NetworkPolicy with podSelector, `policyTypes: [Ingress]` |
| 6 | 5% | Create ServiceAccount `reader`, a Role allowing `get,list,watch` on Pods, and bind it. Verify. | `k create sa/role/rolebinding`, `k auth can-i list pods --as=system:serviceaccount:ns:reader` |
| 7 | 6% | Taint node `node01` with `dedicated=gpu:NoSchedule`. Deploy a Pod that tolerates it and is pinned there via nodeAffinity. | `k taint`, tolerations plus `requiredDuringSchedulingIgnoredDuringExecution` |
| 8 | 7% | Expose Deployment `web` via NodePort 30080, then create an Ingress routing `/api` to Service `api` and `/` to `web`. | `k expose`, Ingress `pathType: Prefix`, check ingressClassName |
| 9 | 6% | Service `shop` has no endpoints. Fix it. | `k get endpoints`, compare selector to Pod labels, check targetPort and readiness |
| 10 | 8% | Install an application with Helm from a given chart in namespace `tools`, override one value, then roll back to the previous revision. | `helm install -n tools --create-namespace --set`, `helm history`, `helm rollback` |

## CKA Mock 2

| # | Weight | Task | Hints |
|---|--------|------|-------|
| 1 | 5% | Create a static Pod `static-web` on `node01` using nginx. | Place manifest in `staticPodPath` from kubelet config |
| 2 | 8% | Add a new worker node to the cluster. | `kubeadm token create --print-join-command`, run on the new node |
| 3 | 8% | New Pods stay `Pending` and no scheduler is running properly. Fix kube-scheduler. | `k -n kube-system get pods`, check `/etc/kubernetes/manifests/kube-scheduler.yaml` for typos in command/paths |
| 4 | 6% | Create a StorageClass `fast` (Retain reclaim policy), make it default, and create a PVC that dynamically provisions. | `storageclass.kubernetes.io/is-default-class` annotation |
| 5 | 8% | Using Gateway API, route traffic for host `shop.example.com` to Service `shop` port 80. | Gateway + HTTPRoute, check `gatewayClassName` and `parentRefs` |
| 6 | 6% | Using Kustomize, create an overlay that sets replicas to 4 and adds a label `env=stage`. | `kustomization.yaml` with `resources`, `patches`, `labels` or `commonLabels`; `k apply -k` |
| 7 | 5% | Identify the Pod using the most CPU in namespace `default` and write its name to a file. | `k top pod --sort-by=cpu`, requires metrics-server |
| 8 | 8% | Pods cannot resolve service names. Diagnose DNS and fix CoreDNS. | `k -n kube-system logs deploy/coredns`, test with busybox `nslookup`, check ConfigMap `coredns` |
| 9 | 6% | Roll out a bad image tag, then roll back to the last working revision and record the reason. | `k rollout history/undo`, `--to-revision` |
| 10 | 6% | In namespace `dev`, apply a ResourceQuota (pods=5, requests.cpu=2) and a LimitRange. Fix a Pod that is rejected. | `k describe quota`, add requests/limits to the Pod |

**Scoring tip:** a task counts only if the final state is correct. Verify with `k get` and `k describe` before moving on.
