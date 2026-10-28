# KCSA Mock Exams

Two 15-question mocks (25 min each). Use Mock 1 as a diagnostic about 7-10 days before the exam and Mock 2 as a dress rehearsal 2-3 days before.

## KCSA Mock 1 (15 questions, 25 min)

1. What are the "4Cs" of cloud native security?
   A. Cloud, Cluster, Container, Code  B. Compute, Cache, Config, Cert  C. Control, Check, Contain, Comply  D. Cluster, Core, CNI, CSI
2. What are the Pod Security Standards levels?
   A. Low, Medium, High  B. Privileged, Baseline, Restricted  C. Open, Closed, Locked  D. Basic, Standard, Strict
3. Which built-in admission controller enforces Pod Security Standards?
   A. Pod Security Admission  B. NodeRestriction only  C. LimitRanger  D. ResourceQuota
4. By default, Secrets in etcd are stored as base64-encoded. What is the key mitigation?
   A. Rename them  B. Enable encryption at rest  C. Use ConfigMaps instead  D. Disable RBAC
5. Which is a valid Kubernetes API authentication method?
   A. Client certificates  B. Anonymous only  C. DNS names  D. Docker credentials
6. With no NetworkPolicy selecting a Pod, what is the default traffic behaviour?
   A. Deny all  B. Allow all  C. Allow only same namespace  D. Allow only egress
7. In STRIDE, what does "E" stand for?
   A. Encryption  B. Elevation of privilege  C. Exposure  D. Escalation of identity
8. Which exposure is most dangerous?
   A. Kubelet API with anonymous auth enabled  B. A ClusterIP service  C. CoreDNS  D. A ConfigMap
9. Which tool scans container images for vulnerabilities?
   A. Trivy  B. Falco  C. Prometheus  D. Fluent Bit
10. Which tool detects suspicious runtime behaviour using system calls?
    A. Falco  B. Trivy  C. Cosign  D. Helm
11. Best practice for RBAC?
    A. Grant cluster-admin to all developers  B. Least privilege with narrowly scoped roles  C. Use wildcards for simplicity  D. Share one ServiceAccount
12. Which Service Account token type is preferred in modern clusters?
    A. Long-lived Secret-based tokens  B. Bound, time-limited projected tokens  C. Static passwords  D. No token
13. What does CIS Kubernetes Benchmark provide?
    A. Hardening recommendations  B. A CNI plugin  C. A package manager  D. A scheduler
14. Which tool family is used to sign and verify container images?
    A. Sigstore / Cosign  B. kubectl  C. kube-proxy  D. CoreDNS
15. Which are Kubernetes policy engines?
    A. OPA Gatekeeper and Kyverno  B. Helm and Kustomize  C. Calico and Cilium  D. containerd and CRI-O

**Answers:** 1-A, 2-B, 3-A, 4-B, 5-A, 6-B, 7-B, 8-A, 9-A, 10-A, 11-B, 12-B, 13-A, 14-A, 15-A

## KCSA Mock 2 (15 questions, 25 min)

1. Which controls best protect etcd?
   A. Mutual TLS, restricted network access, encryption at rest  B. Public endpoint  C. Shared passwords  D. Disabling logs
2. Which settings reduce container escape risk?
   A. Running as root  B. Non-root user, dropped capabilities, seccomp  C. hostPID: true  D. privileged: true
3. What is Kubernetes audit logging used for?
   A. Recording API requests for review and investigation  B. Image building  C. Scaling Pods  D. Pulling images
4. What is an SBOM?
   A. A list of software components in an artifact  B. A secret store  C. A signing key  D. A network map
5. Which NIST publication gives container security guidance?
   A. SP 800-190  B. SP 800-53 only  C. FIPS 140-2 only  D. RFC 2616
6. What does mTLS in a service mesh provide?
   A. Encrypted, mutually authenticated service-to-service traffic  B. Image scanning  C. Node patching  D. Faster scheduling
7. Difference between mutating and validating admission webhooks?
   A. Mutating can modify objects; validating can only accept/reject  B. They are the same  C. Validating changes objects  D. Neither runs on create
8. Why is hostPath risky?
   A. It gives Pods access to the node filesystem  B. It encrypts data  C. It is slower  D. It disables RBAC
9. What typically follows a privileged Pod compromise?
   A. Node-level compromise  B. Nothing  C. Only Pod restart  D. Only DNS failure
10. Kubelet authorization mode that delegates decisions to the API server?
    A. AlwaysAllow  B. Webhook  C. None  D. ABAC-only
11. Are Namespaces a sufficient security boundary on their own?
    A. Yes  B. No, combine with RBAC, NetworkPolicy, quotas and PSS  C. Only with Helm  D. Only with Ingress
12. What does the SLSA framework address?
    A. Supply chain integrity levels  B. Pod scheduling  C. DNS  D. CSI
13. Which are examples of external secrets management?
    A. HashiCorp Vault, External Secrets Operator  B. kubectl proxy  C. kube-proxy  D. Metrics Server
14. Which API server flag disables unauthenticated access?
    A. --anonymous-auth=false  B. --profiling=true  C. --insecure-port=8080  D. --enable-swagger-ui
15. In threat modelling, what is a trust boundary?
    A. A point where data crosses between components of different trust levels  B. A firewall brand  C. A cluster name  D. A namespace quota
    
**Answers:** 1-A, 2-B, 3-A, 4-A, 5-A, 6-A, 7-A, 8-A, 9-A, 10-B, 11-B, 12-A, 13-A, 14-A, 15-A
