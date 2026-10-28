# KCSA Practice Exam: 60 Questions

**Format:** 60 multiple-choice questions, 90 minutes, pass mark about 75% (45/60). No resources allowed.
**Domains (approx. weights):** Overview of Cloud Native Security 14%, Kubernetes Cluster Component Security 22%, Kubernetes Security Fundamentals 22%, Kubernetes Threat Model 16%, Platform Security 16%, Compliance and Security Frameworks 10%.
Questions 1-8 Overview, 9-21 Cluster Components, 22-34 Security Fundamentals, 35-44 Threat Model, 45-54 Platform Security, 55-60 Compliance.
Verify weights against github.com/cncf/curriculum. Answer key at the end.

---

## Overview of Cloud Native Security

**1.** What are the 4Cs of cloud native security, from outermost to innermost?

- A. Code, Container, Cluster, Cloud
- B. Cloud, Container, Cluster, Code
- C. Cluster, Cloud, Code, Container
- D. Cloud, Cluster, Container, Code

**2.** In a managed Kubernetes service, who typically secures the control plane?

- A. The cloud provider
- B. The customer entirely
- C. The application developer
- D. Nobody

**3.** "Defense in depth" means:

- A. Multiple layered controls
- B. One strong control
- C. Hiding the cluster
- D. Disabling logging

**4.** The cloud native security lifecycle phases are:

- A. Code, Compile, Ship
- B. Develop, Distribute, Deploy, Runtime
- C. Install, Run, Stop
- D. Plan, Build, Test, Retire

**5.** The principle of least privilege means:

- A. Deny all access always
- B. Share one account
- C. Grant admin to trusted users
- D. Grant only the permissions needed

**6.** Zero trust is best summarised as:

- A. Trust the internal network
- B. Trust after one login
- C. Never trust, always verify
- D. Trust containers

**7.** What does image provenance tell you?

- A. Its size
- B. Its CPU usage
- C. Where and how an image was built
- D. Its network ports

**8.** Which group publishes the Cloud Native Security Whitepaper?

- A. OWASP only
- B. Docker Inc.
- C. CNCF TAG Security
- D. A cloud vendor only

---

## Kubernetes Cluster Component Security

**9.** Which API server flag sets authorization modes?

- A. --authorization-mode=Node,RBAC
- B. --enable-auth
- C. --authz-file only
- D. --auth=rbac

**10.** What does the NodeRestriction admission plugin do?

- A. Limits kubelets to modifying their own Node and Pods bound to it
- B. Blocks image pulls
- C. Restricts node count
- D. Encrypts etcd

**11.** Which port does etcd use for client requests by default?

- A. 6443
- B. 2380
- C. 2379
- D. 10250

**12.** Which port is the kubelet API on by default?

- A. 2379
- B. 6443
- C. 10250
- D. 8080

**13.** Which component signs certificates for CertificateSigningRequests?

- A. kube-scheduler
- B. CoreDNS
- C. kube-controller-manager
- D. kube-proxy

**14.** Why bind scheduler and controller-manager to localhost where possible?

- A. To disable TLS
- B. To enable anonymous access
- C. To reduce network exposure
- D. To speed scheduling

**15.** What does `--anonymous-auth=false` do on the API server?

- A. Rejects unauthenticated requests
- B. Disables RBAC
- C. Enables audit
- D. Disables TLS

**16.** What is the risk of mounting `/var/run/docker.sock` or the containerd socket into a Pod?

- A. Faster pulls
- B. Container can control the runtime and escape to the node
- C. No risk
- D. DNS failure

**17.** Admission controllers run in what order?

- A. Random
- B. Only validating
- C. Mutating then validating
- D. Validating then mutating

**18.** Which encryption provider means no encryption for Secrets?

- A. secretbox
- B. aescbc
- C. kms
- D. identity

**19.** Which is the kubelet's recommended authorization mode?

- A. ABAC
- B. Webhook
- C. None
- D. AlwaysAllow

**20.** Why disable `--profiling` on control plane components?

- A. Reduce attack surface and information exposure
- B. Reduce etcd size
- C. Enable TLS
- D. Improve scheduling

**21.** The Node authorizer:

- A. Authorises users
- B. Authorises kubelet API requests based on the Pods bound to that node
- C. Authorises images
- D. Authorises Ingress

---

## Kubernetes Security Fundamentals

**22.** Which settings are required by the Restricted Pod Security Standard?

- A. hostNetwork
- B. hostPath volumes
- C. Privileged containers
- D. Run as non-root, drop ALL capabilities, seccomp profile

**23.** What does `allowPrivilegeEscalation: false` do?

- A. Disables RBAC
- B. Blocks network
- C. Prevents a process gaining more privileges than its parent
- D. Blocks DNS

**24.** Which is generally safer for Secrets in Pods?

- A. Image layers
- B. Labels
- C. Mounted volumes
- D. Environment variables

**25.** An empty `podSelector: {}` in a NetworkPolicy:

- A. Is invalid
- B. Selects all Pods in the namespace
- C. Selects all namespaces
- D. Selects no Pods

**26.** Which are RBAC verbs?

- A. read, write
- B. get, list, watch, create, update, patch, delete
- C. start, stop
- D. push, pull

**27.** A ClusterRole bound with a RoleBinding grants access:

- A. Only to nodes
- B. Cluster-wide
- C. Only in the RoleBinding's namespace
- D. Nowhere

**28.** By default, do Pods automount a ServiceAccount token?

- A. Only for admins
- B. Yes unless disabled
- C. Never
- D. Only in kube-system

**29.** What does a ResourceQuota help prevent?

- A. Privilege escalation
- B. DNS spoofing
- C. Image tampering
- D. Resource exhaustion in a namespace

**30.** Which audit levels exist?

- A. Low, Medium, High
- B. Info, Warn, Error
- C. None, Metadata, Request, RequestResponse
- D. Read, Write

**31.** Which are Pod Security Admission modes?

- A. allow, block
- B. strict, loose
- C. on, off
- D. enforce, audit, warn

**32.** Why is `hostNetwork: true` risky?

- A. Slows DNS
- B. Blocks images
- C. Pod shares the node's network namespace
- D. Disables RBAC

**33.** Linux capabilities allow:

- A. Granting specific root privileges individually
- B. DNS caching
- C. Mounting disks only
- D. Image signing

**34.** What does seccomp do?

- A. Routes traffic
- B. Scans images
- C. Encrypts disks
- D. Filters system calls a process can make

---

## Kubernetes Threat Model

**35.** In STRIDE, "Spoofing" refers to:

- A. Impersonating an identity
- B. Reading data
- C. Changing data
- D. Overloading a service

**36.** Which is a common initial-access vector?

- A. A ClusterIP Service
- B. Exposed dashboard or API without authentication
- C. CoreDNS
- D. A Job

**37.** Why is an exposed kubelet API dangerous?

- A. It can allow command execution in Pods
- B. It speeds DNS
- C. It is harmless
- D. It exposes only logs of etcd

**38.** How can a compromised Pod move laterally?

- A. Using its ServiceAccount token and network access
- B. It cannot
- C. Only by DNS
- D. Only by Ingress

**39.** Which RBAC permission can enable privilege escalation?

- A. `watch` on ConfigMaps
- B. `get` on Pods
- C. `list` on Events
- D. `escalate` or `bind` on roles

**40.** What is a supply chain attack?

- A. Node reboot
- B. DNS poisoning only
- C. Network flood
- D. Malicious code introduced via dependencies or images

**41.** Attackers achieve persistence in a cluster by:

- A. Reading a ConfigMap
- B. Creating a CronJob or DaemonSet backdoor
- C. Listing Pods
- D. Using kubectl version

**42.** Missing resource limits can enable:

- A. Denial of service by resource exhaustion
- B. RBAC bypass
- C. Image signing
- D. TLS downgrade

**43.** The cloud metadata service (IMDS) is dangerous when reachable from Pods because:

- A. It routes Services
- B. It slows DNS
- C. It hosts images
- D. It can expose node credentials

**44.** Secrets written to application logs are an example of:

- A. Repudiation
- B. Information disclosure
- C. Tampering
- D. Spoofing

---

## Platform Security

**45.** Which tool signs and verifies container images?

- A. kubectl
- B. CoreDNS
- C. Prometheus
- D. Cosign (Sigstore)

**46.** Which tools scan images for vulnerabilities?

- A. Falco, Cilium
- B. Helm, Kustomize
- C. etcdctl
- D. Trivy, Grype

**47.** Which are Kubernetes policy engines?

- A. OPA Gatekeeper, Kyverno
- B. Calico, Cilium
- C. containerd, CRI-O
- D. Helm, Flux

**48.** Service meshes like Istio and Linkerd commonly provide:

- A. Node patching
- B. Scheduling
- C. Image building
- D. Mutual TLS between services

**49.** Falco detects:

- A. Suspicious runtime behaviour via system call monitoring
- B. DNS records
- C. Image CVEs
- D. YAML syntax errors

**50.** Which are external secrets managers?

- A. kube-proxy
- B. kubectl proxy
- C. HashiCorp Vault, cloud KMS/secret stores
- D. metrics-server

**51.** Which are SBOM formats?

- A. PEM, DER
- B. OCI, CRI
- C. SPDX, CycloneDX
- D. YAML, JSON

**52.** How do Pods pull from a private registry?

- A. NodePorts
- B. ConfigMaps
- C. Labels
- D. Using imagePullSecrets

**53.** What does an eBPF-based CNI such as Cilium enable?

- A. Image signing
- B. Storage
- C. Kernel-level network visibility and policy
- D. DNS only

**54.** Sandboxed runtimes such as gVisor and Kata Containers provide:

- A. Image storage
- B. Faster pulls
- C. Ingress
- D. Stronger isolation between containers and the host kernel

---

## Compliance and Security Frameworks

**55.** What does the CIS Kubernetes Benchmark provide?

- A. Hardening recommendations and checks
- B. A package manager
- C. A CNI plugin
- D. A scheduler

**56.** Which tool automates CIS benchmark checks on nodes?

- A. kubectl-debug
- B. Kustomize
- C. kube-bench
- D. Helm

**57.** NIST SP 800-190 is about:

- A. Password policies only
- B. Application container security guidance
- C. Email security
- D. Network cabling

**58.** "Policy as code" means:

- A. Expressing compliance rules in version-controlled, machine-enforceable form
- B. Disabling audits
- C. Printing policies
- D. Hard-coding passwords

**59.** Why keep Kubernetes audit logs?

- A. They speed up Pods
- B. They encrypt Secrets
- C. They reduce etcd size
- D. They support investigation and compliance evidence

**60.** The NSA/CISA Kubernetes Hardening Guide mainly covers:

- A. Application UX
- B. Hardening guidance for clusters
- C. Image compression
- D. Billing

---

## Answer Key

| Q | A | Why |
|---|---|-----|
| 1 | D | Cloud, Cluster, Container, Code |
| 2 | A | Provider manages the control plane |
| 3 | A | Layered controls |
| 4 | B | Develop, Distribute, Deploy, Runtime |
| 5 | D | Least privilege |
| 6 | C | Never trust, always verify |
| 7 | C | Origin and build record |
| 8 | C | CNCF TAG Security |
| 9 | A | --authorization-mode=Node,RBAC |
| 10 | A | NodeRestriction |
| 11 | C | 2379 client, 2380 peer |
| 12 | C | 10250 |
| 13 | C | Controller manager signer |
| 14 | C | Reduce exposure |
| 15 | A | Rejects anonymous requests |
| 16 | B | Runtime socket gives control of the node |
| 17 | C | Mutating before validating |
| 18 | D | identity = no encryption |
| 19 | B | Webhook |
| 20 | A | Reduce attack surface |
| 21 | B | Node authorizer |
| 22 | D | Restricted profile |
| 23 | C | No privilege gain |
| 24 | C | Volumes safer than env vars |
| 25 | B | All Pods in the namespace |
| 26 | B | RBAC verbs |
| 27 | C | Scoped to namespace |
| 28 | B | Default automount |
| 29 | D | Resource exhaustion |
| 30 | C | Four audit levels |
| 31 | D | enforce/audit/warn |
| 32 | C | Shares node network |
| 33 | A | Fine-grained root powers |
| 34 | D | Syscall filtering |
| 35 | A | Impersonation |
| 36 | B | Exposed unauthenticated interfaces |
| 37 | A | Exec/command execution |
| 38 | A | Token plus network access |
| 39 | D | escalate/bind |
| 40 | D | Malicious dependency/image |
| 41 | B | Backdoor workload |
| 42 | A | DoS |
| 43 | D | Credential exposure |
| 44 | B | Information disclosure |
| 45 | D | Cosign |
| 46 | D | Trivy, Grype |
| 47 | A | Gatekeeper, Kyverno |
| 48 | D | mTLS |
| 49 | A | Runtime detection |
| 50 | C | Vault etc. |
| 51 | C | SPDX, CycloneDX |
| 52 | D | imagePullSecrets |
| 53 | C | eBPF visibility |
| 54 | D | Sandboxed isolation |
| 55 | A | CIS Benchmark |
| 56 | C | kube-bench |
| 57 | B | Container security guidance |
| 58 | A | Policy as code |
| 59 | D | Audit evidence |
| 60 | B | Hardening guide |

**Scoring:** 45+ = pass-ready. Review the domain of every miss.
