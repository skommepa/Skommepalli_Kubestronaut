# CKAD Practice Bank: 60 Hands-On Tasks

**Real exam:** 2 hours, about 15-20 performance-based tasks, pass mark about 66%. kubernetes.io docs allowed (plus Helm docs).
**Domains (approx.):** Application Environment, Configuration & Security 25%, Application Design & Build 20%, Application Deployment 20%, Services & Networking 20%, Application Observability & Maintenance 15%.
Run it as three sets: **A** tasks 1-20, **B** 21-40, **C** 41-60, or mix 15-18 tasks across domains. Solutions are commands and key YAML.

Setup: `alias k=kubectl; export do="--dry-run=client -o yaml"; export now="--force --grace-period=0"`

---

## A. Application Design & Build (Tasks 1-12)

**1.** Create a Pod `web` with image `nginx:1.25` and label `tier=front`.
```
k run web --image=nginx:1.25 --labels=tier=front
```

**2.** Create a Job that runs `echo done`, with 6 completions, parallelism 2, backoffLimit 3.
```
k create job j --image=busybox $do -- echo done > j.yaml
# add under spec: completions: 6, parallelism: 2, backoffLimit: 3
```

**3.** Create a CronJob `report` running every 5 minutes, keeping 2 successful and 1 failed jobs.
```
k create cronjob report --image=busybox --schedule="*/5 * * * *" $do -- date > c.yaml
# add successfulJobsHistoryLimit: 2, failedJobsHistoryLimit: 1
```

**4.** Build an image `app:1.0` from `./Dockerfile` and save it as an OCI archive to `/opt/app.tar`.
```
podman build -t app:1.0 .
podman save --format oci-archive -o /opt/app.tar app:1.0
```

**5.** Create a Pod with an app container and a sidecar sharing an `emptyDir` for logs.
```
volumes: [{name: logs, emptyDir: {}}]
containers:
- {name: app, image: busybox, command: [sh,-c,"while true; do date >> /var/log/app.log; sleep 2; done"], volumeMounts: [{name: logs, mountPath: /var/log}]}
- {name: tail, image: busybox, command: [sh,-c,"tail -F /var/log/app.log"], volumeMounts: [{name: logs, mountPath: /var/log}]}
```

**6.** Add an init container that waits for Service `db` before the app starts.
```
initContainers:
- name: wait
  image: busybox
  command: [sh,-c,"until nslookup db; do sleep 2; done"]
```

**7.** Create a PVC `data` (1Gi, RWO) and mount it at `/data` in a Pod.
```
# PVC then: volumes: [{name: d, persistentVolumeClaim: {claimName: data}}]
```

**8.** Create a Pod with `restartPolicy: Never` that runs a one-off command.
```
k run once --image=busybox --restart=Never -- sh -c "echo hi"
```

**9.** Run a multi-container Pod where the second container is an ambassador proxy on localhost.
```
# two containers in one Pod; they share localhost network namespace
```

**10.** Write a Dockerfile that runs as non-root user 1000.
```
FROM alpine:3.19
RUN adduser -D -u 1000 app
USER 1000
CMD ["sleep","3600"]
```

**11.** Configure a Job to terminate after 60 seconds.
```
spec: {activeDeadlineSeconds: 60}
```

**12.** Create a Pod using a projected volume that combines a ConfigMap and a Secret.
```
volumes:
- name: all
  projected:
    sources:
    - configMap: {name: app-config}
    - secret: {name: app-secret}
```

---

## B. Application Deployment (Tasks 13-24)

**13.** Create Deployment `web` (3 replicas, nginx:1.24) and update to 1.25 with maxSurge=1, maxUnavailable=0.
```
k create deploy web --image=nginx:1.24 --replicas=3 $do > d.yaml
# strategy: {type: RollingUpdate, rollingUpdate: {maxSurge: 1, maxUnavailable: 0}}
k set image deploy/web nginx=nginx:1.25
```

**14.** Roll back `web` to the previous revision.
```
k rollout history deploy/web
k rollout undo deploy/web
```

**15.** Implement a canary: stable (4 replicas) and canary (1 replica) behind one Service.
```
# both Deployments label app=shop; Service selector app=shop;
# distinguish by version label on the Deployment's own selector
```

**16.** Do a blue/green switch by changing a Service selector.
```
k patch svc shop -p '{"spec":{"selector":{"app":"shop","version":"green"}}}'
```

**17.** Install a Helm chart with custom values, upgrade it, and roll back.
```
helm install web repo/chart -f values.yaml
helm upgrade web repo/chart --set image.tag=2.0
helm rollback web 1
helm list
```

**18.** Uninstall a Helm release and list all releases in all namespaces.
```
helm uninstall web -n tools
helm list -A
```

**19.** Use Kustomize to set the image tag and add a ConfigMap generator.
```
resources: [deployment.yaml]
images: [{name: nginx, newTag: "1.25"}]
configMapGenerator: [{name: cfg, literals: [MODE=prod]}]
k apply -k .
```

**20.** Scale Deployment `web` to 6 replicas and pause/resume a rollout.
```
k scale deploy web --replicas=6
k rollout pause deploy/web; k rollout resume deploy/web
```

**21.** Create an HPA for `web` (min 2, max 5, CPU 60%).
```
k autoscale deploy web --min=2 --max=5 --cpu-percent=60
```

**22.** Record a change cause on a rollout.
```
k annotate deploy web kubernetes.io/change-cause="upgrade to 1.25"
```

**23.** Change a Deployment's strategy to Recreate.
```
spec: {strategy: {type: Recreate}}
```

**24.** Create a Deployment from a given YAML whose API version is deprecated; fix and apply.
```
k explain deploy      # confirm apps/v1
# change apiVersion to apps/v1 and add spec.selector.matchLabels
```

---

## C. Application Observability & Maintenance (Tasks 25-33)

**25.** Add an HTTP liveness probe on `/healthz:8080` to a Deployment.
```
livenessProbe: {httpGet: {path: /healthz, port: 8080}, initialDelaySeconds: 5, periodSeconds: 10}
```

**26.** Add a TCP readiness probe on port 3306.
```
readinessProbe: {tcpSocket: {port: 3306}, periodSeconds: 5}
```

**27.** Add a startup probe allowing up to 5 minutes for boot.
```
startupProbe: {httpGet: {path: /healthz, port: 8080}, failureThreshold: 30, periodSeconds: 10}
```

**28.** Get logs of a crashed container's previous instance.
```
k logs <pod> --previous
```

**29.** Find the Pod using the most memory in namespace `apps`.
```
k top pod -n apps --sort-by=memory
```

**30.** A Pod is in ImagePullBackOff; fix it.
```
k describe pod <p>; k set image deploy/x c=<valid-image>
```

**31.** A Pod is in CrashLoopBackOff; find and fix the cause.
```
k logs <p> --previous; k describe pod <p>
# typical causes: wrong command, missing ConfigMap/Secret, failing probe
```

**32.** Open a debug shell and test connectivity to a Service.
```
k run dbg --image=busybox:1.36 --rm -it --restart=Never -- wget -qO- http://web:80
k exec -it <pod> -- sh
```

**33.** Save cluster events for a namespace sorted by time.
```
k get events -n apps --sort-by=.metadata.creationTimestamp > /opt/ev.txt
```

---

## D. Application Environment, Configuration & Security (Tasks 34-48)

**34.** Create ConfigMap `app-config` from literals and a file.
```
k create cm app-config --from-literal=MODE=prod --from-file=app.properties
```

**35.** Create Secret `app-secret` and expose a key as env var `DB_PASS`.
```
k create secret generic app-secret --from-literal=password=s3cr3t
# env: [{name: DB_PASS, valueFrom: {secretKeyRef: {name: app-secret, key: password}}}]
```

**36.** Mount ConfigMap as files at `/etc/config`.
```
volumes: [{name: c, configMap: {name: app-config}}]
volumeMounts: [{name: c, mountPath: /etc/config}]
```

**37.** Load all keys of a ConfigMap as env vars.
```
envFrom: [{configMapRef: {name: app-config}}]
```

**38.** Run a Pod as UID 1000 with a read-only root filesystem.
```
securityContext: {runAsUser: 1000, readOnlyRootFilesystem: true}
```

**39.** Drop all capabilities and add only `NET_BIND_SERVICE`.
```
securityContext: {capabilities: {drop: [ALL], add: [NET_BIND_SERVICE]}}
```

**40.** Set `allowPrivilegeEscalation: false` and `runAsNonRoot: true`.
```
securityContext: {runAsNonRoot: true, allowPrivilegeEscalation: false}
```

**41.** Create ServiceAccount `app-sa` and run a Pod with it; disable token automount.
```
k create sa app-sa
# pod: serviceAccountName: app-sa, automountServiceAccountToken: false
```

**42.** Give `app-sa` read access to ConfigMaps in its namespace.
```
k create role cm-read --verb=get,list --resource=configmaps
k create rolebinding cm-read --role=cm-read --serviceaccount=<ns>:app-sa
```

**43.** Set requests and limits on a container.
```
resources: {requests: {cpu: 100m, memory: 64Mi}, limits: {cpu: 200m, memory: 128Mi}}
```

**44.** Create a ResourceQuota (pods=5, requests.cpu=2) in `dev`.
```
k create quota q --hard=pods=5,requests.cpu=2 -n dev
```

**45.** Create a LimitRange giving default container limits.
```
apiVersion: v1
kind: LimitRange
metadata: {name: lr}
spec:
  limits: [{type: Container, default: {cpu: 200m, memory: 128Mi}, defaultRequest: {cpu: 100m, memory: 64Mi}}]
```

**46.** A Pod was OOMKilled; raise the memory limit.
```
k describe pod <p>      # Last State: OOMKilled
# increase limits.memory and re-apply
```

**47.** Create an instance of an existing CRD.
```
k get crd; k explain <kind>.spec
# write CR YAML and k apply -f
```

**48.** Use a downward API env var to expose the Pod name.
```
env: [{name: POD_NAME, valueFrom: {fieldRef: {fieldPath: metadata.name}}}]
```

---

## E. Services & Networking (Tasks 49-60)

**49.** Expose Deployment `web` as ClusterIP on port 80.
```
k expose deploy web --port=80 --target-port=8080
```

**50.** Expose as NodePort 30080.
```
k expose deploy web --type=NodePort --port=80 $do > s.yaml   # set nodePort: 30080
```

**51.** Create an Ingress for host `app.local` to Service `web:80`.
```
k create ingress app --rule="app.local/*=web:80" --class=nginx
```

**52.** Allow only Pods `role=frontend` to reach `role=backend`.
```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata: {name: be}
spec:
  podSelector: {matchLabels: {role: backend}}
  policyTypes: [Ingress]
  ingress: [{from: [{podSelector: {matchLabels: {role: frontend}}}]}]
```

**53.** Default-deny all ingress in a namespace.
```
spec: {podSelector: {}, policyTypes: [Ingress]}
```

**54.** An Ingress returns 503; fix Service targetPort/selector mismatch.
```
k get ep <svc>; k describe svc <svc>
k get pods --show-labels
```

**55.** Test a Service from a temporary Pod.
```
k run t --image=curlimages/curl --rm -it --restart=Never -- curl -s http://web.<ns>.svc
```

**56.** Allow egress from `app=api` only to port 5432 on `app=db`.
```
policyTypes: [Egress]
egress: [{to: [{podSelector: {matchLabels: {app: db}}}], ports: [{port: 5432}]}]
```

**57.** Create a Service with named port and reference it in the Pod.
```
# container ports: [{name: http, containerPort: 8080}]; Service targetPort: http
```

**58.** Expose a Pod directly with a Service.
```
k expose pod web --port=80 --name=web-svc
```

**59.** Port-forward a Service locally and test it.
```
k port-forward svc/web 8080:80 &
curl localhost:8080
```

**60.** Add a second path to an existing Ingress.
```
k edit ingress app    # add a path with pathType: Prefix and backend service
```

---

## Self-review sheet
For each missed task: Task # | What failed | Correct approach | Doc page.
