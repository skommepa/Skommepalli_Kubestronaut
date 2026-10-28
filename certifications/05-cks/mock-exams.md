# CKS Mock Exams

Practice in a cluster where you can edit static pod manifests, install Falco and Trivy, and load AppArmor profiles on a node. Reach for the KodeKloud CKS labs and challenges for the environment.

## CKS Mock 1

| # | Weight | Task | Hints |
|---|--------|------|-------|
| 1 | 6% | In namespace `secure`, apply a default-deny NetworkPolicy (ingress and egress), then allow DNS egress and Pods `app=web` to reach `app=api` on 8080. | Empty `podSelector`, allow UDP/TCP 53 to kube-dns |
| 2 | 8% | Run `kube-bench`, fix the listed API server failures (for example `--anonymous-auth=false`, `--profiling=false`). | Edit `/etc/kubernetes/manifests/kube-apiserver.yaml`, wait for restart |
| 3 | 7% | Remove wildcard permissions from a Role, and restrict a ServiceAccount to read-only Pods. | `k get role -o yaml`, rewrite rules |
| 4 | 7% | Load AppArmor profile `k8s-deny-write` on `node01` and enforce it for a Pod. | `apparmor_parser -q`, annotation or `securityContext.appArmorProfile` depending on version |
| 5 | 7% | Apply the `RuntimeDefault` seccomp profile to a Deployment, and a custom profile to a second Pod. | `securityContext.seccompProfile`, Localhost path under kubelet seccomp dir |
| 6 | 7% | Label namespace `prod` with `pod-security.kubernetes.io/enforce=restricted` and fix a Pod that is rejected. | Non-root, `allowPrivilegeEscalation: false`, drop ALL, seccomp |
| 7 | 8% | Use Trivy to scan the images in namespace `apps`. Delete Pods running images with HIGH or CRITICAL vulnerabilities. | `trivy image --severity HIGH,CRITICAL` |
| 8 | 8% | Use Falco to find the Pod spawning a shell, and update a rule's output format. Delete the offending Pod. | `/etc/falco/falco_rules.local.yaml`, `journalctl -u falco` |
| 9 | 7% | Enable API server audit logging with a policy that logs `Metadata` for Secrets and `RequestResponse` for Pods. | `--audit-policy-file`, `--audit-log-path`, mount hostPath volumes |
| 10 | 8% | Enable encryption at rest for Secrets and re-encrypt existing ones. | `EncryptionConfiguration`, `--encryption-provider-config`, `k get secrets -A -o json \| k replace -f -` |

## CKS Mock 2

| # | Weight | Task | Hints |
|---|--------|------|-------|
| 1 | 7% | Fix a Dockerfile (unpinned base image, running as root) and a manifest flagged by kubesec. | Pin tag/digest, `USER 1000`, drop capabilities |
| 2 | 8% | Enforce an allowed-registries rule using OPA Gatekeeper or Kyverno. | ConstraintTemplate + Constraint, or Kyverno ClusterPolicy |
| 3 | 7% | Create RuntimeClass `gvisor` (handler `runsc`) and run a Pod with it. | `runtimeClassName` |
| 4 | 6% | Create a TLS Secret and configure Ingress TLS. | `k create secret tls`, `spec.tls` |
| 5 | 6% | Disable automatic SA token mounting in a namespace and grant minimal RBAC where needed. | Patch default ServiceAccount |
| 6 | 8% | Harden the kubelet on `node01` (anonymous auth off, authorization Webhook), then verify. | `/var/lib/kubelet/config.yaml`, restart kubelet |
| 7 | 7% | Find a service listening on an unexpected port on a node, and stop and disable it. | `ss -tlnp`, `systemctl disable --now` |
| 8 | 6% | Verify the sha512 checksum of a kubelet binary against the provided value. | `sha512sum`, compare |
| 9 | 8% | Investigate a suspicious Pod with Falco/Sysdig output, and remove it and its Deployment. | Delete the controller, not just the Pod |
| 10 | 8% | Make a Pod's root filesystem read-only, with `emptyDir` for the one writable path. | `readOnlyRootFilesystem: true` |
