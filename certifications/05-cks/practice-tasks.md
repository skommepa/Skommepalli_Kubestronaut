# CKS Practice Bank: 60 Hands-On Tasks

**Real exam:** 2 hours, about 15-20 performance-based tasks, pass mark about 67%. Requires an active CKA. Allowed docs: kubernetes.io plus documentation for tools such as Trivy, Falco and AppArmor (check the current candidate handbook).
**Domains (approx.):** Minimize Microservice Vulnerabilities 20%, Supply Chain Security 20%, Monitoring/Logging/Runtime Security 20%, Cluster Hardening 15%, Cluster Setup 10%, System Hardening 10%.
Run it as three sets: **A** tasks 1-20, **B** 21-40, **C** 41-60. Solutions are key commands and YAML; versions and paths vary by lab.

Setup: `alias k=kubectl; export do="--dry-run=client -o yaml"`

---

## A. Cluster Setup (Tasks 1-6)

**1.** In namespace `secure`, apply default-deny for ingress and egress, then allow DNS egress.
```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata: {name: default-deny, namespace: secure}
spec: {podSelector: {}, policyTypes: [Ingress, Egress]}
---
metadata: {name: allow-dns, namespace: secure}
spec:
  podSelector: {}
  policyTypes: [Egress]
  egress:
  - to: [{namespaceSelector: {}}]
    ports: [{protocol: UDP, port: 53}, {protocol: TCP, port: 53}]
```

**2.** Block Pod access to the cloud metadata endpoint `169.254.169.254`.
```
egress: [{to: [{ipBlock: {cidr: 0.0.0.0/0, except: [169.254.169.254/32]}}]}]
```

**3.** Run kube-bench and fix API server failures (anonymous auth, profiling).
```
kube-bench run --targets master
# edit /etc/kubernetes/manifests/kube-apiserver.yaml:
#   --anonymous-auth=false   --profiling=false
```

**4.** Configure Ingress TLS using a new TLS Secret.
```
k create secret tls web-tls --cert=tls.crt --key=tls.key
# ingress spec.tls: [{hosts: [web.example.com], secretName: web-tls}]
```

**5.** Verify a downloaded kubelet binary's checksum against the supplied value.
```
sha512sum kubelet | grep <expected>
```

**6.** Restrict access to the Kubernetes Dashboard: make it ClusterIP and remove cluster-admin from its ServiceAccount.
```
k -n kubernetes-dashboard patch svc kubernetes-dashboard -p '{"spec":{"type":"ClusterIP"}}'
k delete clusterrolebinding <dashboard-admin-binding>
```

---

## B. Cluster Hardening (Tasks 7-15)

**7.** Remove wildcards from a Role.
```
k get role r -o yaml     # replace verbs/resources "*" with explicit lists
k edit role r
```

**8.** Disable ServiceAccount token automount in namespace `app`.
```
k -n app patch sa default -p '{"automountServiceAccountToken": false}'
```

**9.** Restrict a ServiceAccount to read-only access on Pods.
```
k create role pod-read --verb=get,list,watch --resource=pods
k create rolebinding sa-pod-read --role=pod-read --serviceaccount=app:sa1
```

**10.** Enable the NodeRestriction admission plugin.
```
# kube-apiserver: --enable-admission-plugins=NodeRestriction
```

**11.** Ensure the API server rejects anonymous requests and the insecure port is off.
```
--anonymous-auth=false   # insecure port flag was removed in modern versions; verify no http port is exposed
```

**12.** Harden kubelet on `node01`: anonymous auth off, Webhook authorization.
```
# /var/lib/kubelet/config.yaml
authentication: {anonymous: {enabled: false}, webhook: {enabled: true}}
authorization: {mode: Webhook}
systemctl restart kubelet
```

**13.** Upgrade a cluster to patch a known CVE (one minor version).
```
kubeadm upgrade plan; kubeadm upgrade apply v<ver>   # then kubelet upgrade per node
```

**14.** Create a user via CSR limited to read access in one namespace.
```
# CSR signerName kubernetes.io/kube-apiserver-client; approve
k create role r --verb=get,list --resource=pods -n dev
k create rolebinding rb --role=r --user=dev1 -n dev
```

**15.** Find which ClusterRoleBindings grant cluster-admin and remove unnecessary ones.
```
k get clusterrolebinding -o wide | grep cluster-admin
k delete clusterrolebinding <name>
```

---

## C. System Hardening (Tasks 16-21)

**16.** Load AppArmor profile `k8s-deny-write` on `node01` and apply it to a Pod.
```
apparmor_parser -q /etc/apparmor.d/k8s-deny-write
# k8s 1.30+: securityContext: {appArmorProfile: {type: Localhost, localhostProfile: k8s-deny-write}}
# older: annotation container.apparmor.security.beta.kubernetes.io/<c>: localhost/k8s-deny-write
```

**17.** Apply the RuntimeDefault seccomp profile to a Deployment.
```
securityContext: {seccompProfile: {type: RuntimeDefault}}
```

**18.** Apply a custom seccomp profile stored on the node.
```
securityContext: {seccompProfile: {type: Localhost, localhostProfile: profiles/audit.json}}
# file at /var/lib/kubelet/seccomp/profiles/audit.json
```

**19.** Find and stop an unexpected service listening on a node port.
```
ss -tlnp
systemctl disable --now <service>
```

**20.** Remove an unneeded package that exposes a service.
```
apt-get remove -y <pkg>
```

**21.** Restrict SSH on a node to key authentication only.
```
# /etc/ssh/sshd_config: PasswordAuthentication no; PermitRootLogin no
systemctl restart sshd
```

---

## D. Minimize Microservice Vulnerabilities (Tasks 22-33)

**22.** Enforce the `restricted` Pod Security Standard on namespace `prod`.
```
k label ns prod pod-security.kubernetes.io/enforce=restricted
```

**23.** A Pod is rejected by PSA; make it compliant.
```
securityContext: {runAsNonRoot: true, allowPrivilegeEscalation: false, capabilities: {drop: [ALL]}, seccompProfile: {type: RuntimeDefault}}
```

**24.** Remove `privileged: true` from a Pod and drop capabilities.
```
securityContext: {privileged: false, capabilities: {drop: [ALL]}}
```

**25.** Remove a `hostPath` mount of `/` from a Pod and replace with emptyDir.
```
volumes: [{name: tmp, emptyDir: {}}]
```

**26.** Run a Pod under gVisor using a RuntimeClass.
```
apiVersion: node.k8s.io/v1
kind: RuntimeClass
metadata: {name: gvisor}
handler: runsc
# pod: runtimeClassName: gvisor
```

**27.** Make a Pod's root filesystem read-only, with writable `/tmp` via emptyDir.
```
securityContext: {readOnlyRootFilesystem: true}
volumeMounts: [{name: tmp, mountPath: /tmp}]
```

**28.** Enable encryption at rest for Secrets.
```
# /etc/kubernetes/enc/enc.yaml
apiVersion: apiserver.config.k8s.io/v1
kind: EncryptionConfiguration
resources:
- resources: [secrets]
  providers:
  - aescbc: {keys: [{name: key1, secret: <base64-32-byte-key>}]}
  - identity: {}
# kube-apiserver: --encryption-provider-config=/etc/kubernetes/enc/enc.yaml (mount the dir)
k get secrets -A -o json | k replace -f -
```

**29.** Verify a Secret is encrypted in etcd.
```
ETCDCTL_API=3 etcdctl get /registry/secrets/default/s1 [certs flags] | hexdump -C | head
# value should start with k8s:enc:aescbc:v1:key1
```

**30.** Restrict Pods to mTLS using the service mesh/CNI feature provided in the lab.
```
# e.g. Istio PeerAuthentication mode STRICT, or Cilium mutual authentication policy per lab docs
```

**31.** Set CPU/memory limits and a namespace ResourceQuota to limit DoS risk.
```
k create quota q --hard=cpu=4,memory=4Gi,pods=10 -n prod
```

**32.** Stop mounting Secrets as env vars; mount as files instead.
```
volumes: [{name: s, secret: {secretName: db}}]
volumeMounts: [{name: s, mountPath: /etc/secret, readOnly: true}]
```

**33.** Limit a ServiceAccount from creating Pods.
```
# remove create on pods from its Role; verify with k auth can-i create pods --as=system:serviceaccount:ns:sa
```

---

## E. Supply Chain Security (Tasks 34-45)

**34.** Scan all images in namespace `apps` with Trivy and list HIGH/CRITICAL findings.
```
for i in $(k -n apps get pods -o jsonpath='{..image}' | tr ' ' '\n' | sort -u); do
  trivy image --severity HIGH,CRITICAL $i; done
```

**35.** Delete Pods that run images with CRITICAL vulnerabilities.
```
k -n apps delete deploy <name>      # delete the controller, not only the Pod
```

**36.** Restrict images to the registry `registry.local` with OPA Gatekeeper.
```
# ConstraintTemplate K8sAllowedRepos + Constraint with repos: ["registry.local/"]
```

**37.** Restrict images using a Kyverno ClusterPolicy.
```
validate:
  message: "Only registry.local images are allowed"
  pattern:
    spec:
      containers:
      - image: "registry.local/*"
```

**38.** Configure the ImagePolicyWebhook admission plugin.
```
# kube-apiserver: --enable-admission-plugins=...,ImagePolicyWebhook
# --admission-control-config-file=/etc/kubernetes/admission/config.yaml
# config sets kubeConfigFile, allowTTL, defaultAllow: false
```

**39.** Fix a Dockerfile: pin the base image, drop root, remove `latest`.
```
FROM alpine:3.19.1
RUN adduser -D -u 1000 app
USER 1000
```

**40.** Run kubesec on a manifest and fix the failed checks.
```
kubesec scan pod.yaml
# add runAsNonRoot, readOnlyRootFilesystem, resource limits, drop ALL capabilities
```

**41.** Use image digests rather than tags in a Deployment.
```
image: registry.local/app@sha256:<digest>
```

**42.** Create an `imagePullSecret` for a private registry and use it.
```
k create secret docker-registry reg --docker-server=registry.local --docker-username=u --docker-password=p
# pod: imagePullSecrets: [{name: reg}]
```

**43.** Verify an image signature with Cosign.
```
cosign verify --key cosign.pub registry.local/app:1.0
```

**44.** Generate an SBOM for an image.
```
trivy image --format cyclonedx -o sbom.json registry.local/app:1.0
```

**45.** Reject a Deployment using the `latest` tag with a policy.
```
# Kyverno: pattern image: "!*:latest"  | Gatekeeper: custom Rego constraint
```

---

## F. Monitoring, Logging & Runtime Security (Tasks 46-60)

**46.** Find the process that spawned a shell in a container using Falco.
```
journalctl -u falco -n 100 | grep -i shell
# or: grep "shell" /var/log/falco.log
```

**47.** Change the output format of a Falco rule.
```
# /etc/falco/falco_rules.local.yaml: override the rule's output field
systemctl restart falco
```

**48.** Add a custom Falco rule that alerts on writes to `/etc`.
```
- rule: Write below etc
  desc: detect writes under /etc
  condition: evt.type in (open, openat) and evt.is_open_write=true and fd.name startswith /etc
  output: "File write under /etc (user=%user.name file=%fd.name container=%container.name)"
  priority: WARNING
```

**49.** Enable API server audit logging with a policy.
```
# audit-policy.yaml
apiVersion: audit.k8s.io/v1
kind: Policy
rules:
- level: Metadata
  resources: [{group: "", resources: ["secrets"]}]
- level: RequestResponse
  resources: [{group: "", resources: ["pods"]}]
- level: None
# kube-apiserver flags:
--audit-policy-file=/etc/kubernetes/audit-policy.yaml
--audit-log-path=/var/log/kubernetes/audit.log
--audit-log-maxage=7 --audit-log-maxbackup=3
# add hostPath volumes/mounts for both paths
```

**50.** Find who deleted a Pod from the audit log.
```
grep '"verb":"delete"' /var/log/kubernetes/audit.log | grep '"resource":"pods"' | jq '.user.username'
```

**51.** Identify a Pod running an unexpected process using `crictl`.
```
crictl ps; crictl inspect <id> | jq '.info.pid'
ps -ef | grep <pid>
```

**52.** Remove a compromised Pod and its owning Deployment.
```
k get pod <p> -o jsonpath='{.metadata.ownerReferences}'
k delete deploy <name>
```

**53.** Make containers immutable: read-only root filesystem and no shell tools.
```
securityContext: {readOnlyRootFilesystem: true}
```

**54.** Find Pods mounting host paths or using hostNetwork.
```
k get pods -A -o json | jq -r '.items[] | select(.spec.hostNetwork==true) | .metadata.name'
k get pods -A -o json | jq -r '.items[] | select(.spec.volumes[]?.hostPath) | .metadata.name'
```

**55.** Find Pods running as root.
```
k get pods -A -o json | jq -r '.items[] | select(.spec.securityContext.runAsNonRoot != true) | .metadata.name'
```

**56.** Detect a container writing to a sensitive file and terminate it.
```
# identify via Falco output; delete the Pod/Deployment
```

**57.** Rotate the audit log and keep 5 backups.
```
--audit-log-maxbackup=5 --audit-log-maxsize=100
```

**58.** List Secrets accessed in the last hour from the audit log.
```
jq 'select(.objectRef.resource=="secrets")' /var/log/kubernetes/audit.log | tail
```

**59.** Check for Pods created by unexpected users.
```
jq -r 'select(.verb=="create" and .objectRef.resource=="pods") | .user.username' /var/log/kubernetes/audit.log | sort | uniq -c
```

**60.** Review a Falco alert, then harden the Pod that caused it.
```
# add readOnlyRootFilesystem, drop capabilities, enforce AppArmor/seccomp, redeploy
```

---

## Self-review sheet
For each missed task: Task # | What failed | Correct approach | Doc page.
