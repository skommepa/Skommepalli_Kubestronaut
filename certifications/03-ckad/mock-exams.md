# CKAD Mock Exams

Two 10-task hands-on mocks. Use Mock 1 as a diagnostic and Mock 2 as a timed dress rehearsal (docs only).

## CKAD Mock 1

| # | Weight | Task | Hints |
|---|--------|------|-------|
| 1 | 6% | Create CronJob `report` running busybox every 5 minutes, keeping 2 successful and 1 failed job history. | `k create cronjob`, edit history limits |
| 2 | 8% | Build a Pod with an app container writing to `/var/log/app.log` and a sidecar tailing it, sharing an `emptyDir`. | Two containers, one volume, two volumeMounts |
| 3 | 6% | Build an image from a given Dockerfile with podman, tag `app:1.0`, save as an OCI archive to `/opt/app.tar`. | `podman build -t`, `podman save --format oci-archive -o` |
| 4 | 8% | Update Deployment `web` with `maxSurge=1`, `maxUnavailable=0`. Roll to a new image, then roll back. | `k set image`, `k rollout undo`, strategy in spec |
| 5 | 8% | Create ConfigMap `app-config` and Secret `app-secret`. Inject one as env vars and the other as a mounted volume. | `k create cm/secret --from-literal`, `envFrom`, volume mounts |
| 6 | 8% | Run a Pod as user 1000, with `readOnlyRootFilesystem: true`, dropping all capabilities except `NET_BIND_SERVICE`. | `securityContext` at Pod and container level |
| 7 | 8% | Add liveness (HTTP), readiness (TCP) and startup probes to a Deployment. | Check `initialDelaySeconds`, `periodSeconds`, `failureThreshold` |
| 8 | 6% | Create a ClusterIP Service and an Ingress for host `app.local`. | Service port vs targetPort, ingressClassName |
| 9 | 6% | Allow only Pods labelled `role=frontend` to reach Pods labelled `role=backend`. | NetworkPolicy podSelector |
| 10 | 5% | Create a ServiceAccount, and run a Pod with it. Set CPU/memory requests and limits. | `serviceAccountName`, resources block |

## CKAD Mock 2

| # | Weight | Task | Hints |
|---|--------|------|-------|
| 1 | 6% | Create a Job with `completions: 6`, `parallelism: 2`, `backoffLimit: 3`. | `k create job`, edit spec |
| 2 | 6% | Add an init container that waits for Service `db` to resolve before the app starts. | `until nslookup db; do sleep 2; done` |
| 3 | 8% | Implement a canary: two Deployments behind one Service, ~80/20 split by replica count. | Shared label for Service selector, different version labels |
| 4 | 8% | Install a Helm chart, upgrade with new values, list releases, roll back. | `helm install/upgrade/rollback/list` |
| 5 | 6% | Use Kustomize to patch image tag and add a ConfigMap generator. | `configMapGenerator`, `images:` transformer |
| 6 | 8% | A Pod is in `ImagePullBackOff` and another `CrashLoopBackOff`. Find and fix both. | `k describe`, `k logs --previous`, `k get events` |
| 7 | 6% | Create a CustomResourceDefinition instance from an existing CRD. | `k get crd`, `k explain`, write the CR |
| 8 | 8% | A Pod keeps getting OOMKilled. Adjust limits and add a LimitRange to prevent recurrence. | `k describe pod` (Reason), memory limits |
| 9 | 6% | Disable token automount for a ServiceAccount and give another one a Role to read ConfigMaps. | `automountServiceAccountToken: false`, Role + RoleBinding |
| 10 | 8% | An Ingress returns 503. Fix Service port/targetPort and endpoint mismatch. | `k get ep`, compare ports and labels |
