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

## Files

- [practice-tasks.md](practice-tasks.md): 60 hands-on tasks with key commands and YAML (versions and paths vary by lab)
- [mock-exams.md](mock-exams.md): two 10-task mocks

## Lab requirements

A cluster where you can edit static Pod manifests, install Falco and Trivy, and load AppArmor profiles on a node. The KodeKloud CKS labs and challenges provide this.

## Milestone

KodeKloud CKS challenges plus both mocks done, then sit CKS. Use the retake window if needed.
