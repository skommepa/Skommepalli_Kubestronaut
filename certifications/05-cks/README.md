# Module 5: CKS (Certified Kubernetes Security Specialist)

**Duration:** 16 weeks (weeks 28-43, months 7-10): a 4-week gap, 9 weeks of study, 3 weeks for the retake | **Previous:** [KCSA](../04-kcsa/) | **Then:** claim Kubestronaut

**Prerequisite:** an active CKA.

## Exam facts

| | |
|---|---|
| Format | Hands-on terminal tasks, ~15-20 tasks |
| Time | 2 hours |
| Pass mark | ~67% |
| Resources | kubernetes.io docs plus tool docs (Trivy, Falco, AppArmor); check the current candidate handbook |

## Domains (approximate weights)

| Domain | Weight | Practice tasks |
|--------|--------|----------------|
| Minimize Microservice Vulnerabilities | 20% | 22-33 |
| Supply Chain Security | 20% | 34-45 |
| Monitoring, Logging & Runtime Security | 20% | 46-60 |
| Cluster Hardening | 15% | 7-15 |
| Cluster Setup | 10% | 1-6 |
| System Hardening | 10% | 16-21 |

## Plan

CKS took me two attempts, so it gets a 1-month gap before it and a retake window after it.

| Weeks | Focus |
|-------|-------|
| 28-31 (gap) | One month of extra preparation: set up Falco, Trivy and AppArmor labs, rehearse editing static Pod manifests |
| 32-33 | Cluster setup and hardening: NetworkPolicy, kube-bench, RBAC, kubelet and API server flags |
| 34 | System hardening: AppArmor, seccomp, host services |
| 35-36 | Microservice security: Pod Security Admission, RuntimeClass (gVisor), encryption at rest, mTLS |
| 37 | Supply chain: Trivy, Kyverno/Gatekeeper, ImagePolicyWebhook, Cosign, SBOM |
| 38 | Runtime: Falco rules, audit logging, forensics with crictl |
| 39-40 | KodeKloud CKS challenges, timed mocks, review every miss, first exam attempt |
| 41-43 | Retake window: review the domains you scored lowest in, then retake |

## Learning path

**KodeKloud courses (in this order)**

1. [Certified Kubernetes Security Specialist (CKS)](https://learn.kodekloud.com/learn/courses/certified-kubernetes-security-specialist-cks)
2. [CKS - Challenges](https://learn.kodekloud.com/learn/courses/cks-challenges)

**Official and public resources**

- [CKS exam page (Linux Foundation)](https://training.linuxfoundation.org/certification/certified-kubernetes-security-specialist/) and [CNCF certification page](https://www.cncf.io/training/certification/cks/)
- [Official CKS curriculum](https://github.com/cncf/curriculum): use the CKS PDF to check domains and weights
- [Kubernetes security checklist](https://kubernetes.io/docs/concepts/security/security-checklist/)
- [Network policies](https://kubernetes.io/docs/concepts/services-networking/network-policies/)
- [Pod Security Admission](https://kubernetes.io/docs/concepts/security/pod-security-admission/) and [Pod Security Standards](https://kubernetes.io/docs/concepts/security/pod-security-standards/)
- [Restrict a container's access with AppArmor](https://kubernetes.io/docs/tutorials/security/apparmor/)
- [Restrict a container's syscalls with seccomp](https://kubernetes.io/docs/tutorials/security/seccomp/)
- [Encrypting confidential data at rest](https://kubernetes.io/docs/tasks/administer-cluster/encrypt-data/)
- [Auditing](https://kubernetes.io/docs/tasks/debug/debug-cluster/audit/)
- [Runtime classes (gVisor, Kata)](https://kubernetes.io/docs/concepts/containers/runtime-class/)
- [Admission controllers](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/)
- Tools allowed in the exam docs: [Trivy](https://trivy.dev/), [Falco](https://falco.org/docs/), [kube-bench](https://github.com/aquasecurity/kube-bench), [Kyverno](https://kyverno.io/docs/), [OPA Gatekeeper](https://open-policy-agent.github.io/gatekeeper/website/docs/), [Sigstore / Cosign](https://docs.sigstore.dev/). Check the current candidate handbook for the exact allowed list.

## Files

- [practice-tasks.md](practice-tasks.md): 60 hands-on tasks with key commands and YAML (versions and paths vary by lab)
- [mock-exams.md](mock-exams.md): two 10-task mocks

## Lab requirements

A cluster where you can edit static Pod manifests, install Falco and Trivy, and load AppArmor profiles on a node. The KodeKloud CKS labs and challenges provide this.

## Milestone

KodeKloud CKS challenges plus both mocks done, then sit CKS. Use the retake window if needed.
