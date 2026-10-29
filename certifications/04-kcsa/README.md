# Module 4: KCSA (Kubernetes and Cloud Native Security Associate)

**Duration:** 3 weeks (weeks 25-27, months 6-7) | **Previous:** [CKAD](../03-ckad/) | **Next:** [Module 5: CKS](../05-cks/)

## Exam facts

| | |
|---|---|
| Format | ~60 multiple-choice questions, online proctored |
| Time | 90 minutes |
| Pass mark | ~75% (45/60) |
| Resources | None |

## Domains (approximate weights)

| Domain | Weight | Practice questions |
|--------|--------|--------------------|
| Overview of Cloud Native Security | 14% | 1-8 |
| Kubernetes Cluster Component Security | 22% | 9-21 |
| Kubernetes Security Fundamentals | 22% | 22-34 |
| Kubernetes Threat Model | 16% | 35-44 |
| Platform Security | 16% | 45-54 |
| Compliance and Security Frameworks | 10% | 55-60 |

## Plan

- **Weeks 1-2:** 45-60 min a day on one domain plus 15-20 practice questions.
- **Week 3:** Take [Mock 1](mock-exams.md), fix weak domains, then take Mock 2 and the full [60-question bank](practice-questions.md).

This module doubles as the concept primer for CKS, so take notes on the tools (Trivy, Falco, Cosign, Kyverno, Gatekeeper).

## Learning path

**KodeKloud course**

1. [Kubernetes and Cloud Native Security Associate (KCSA)](https://learn.kodekloud.com/learn/courses/kubernetes-and-cloud-native-security-associate-kcsa)

**Official and public resources**

- [KCSA exam page (Linux Foundation)](https://training.linuxfoundation.org/certification/kubernetes-and-cloud-native-security-associate-kcsa/) and [CNCF certification page](https://www.cncf.io/training/certification/kcsa/)
- [Official KCSA curriculum](https://github.com/cncf/curriculum): use the KCSA PDF to check domains and weights
- [Kubernetes security overview (the 4Cs)](https://kubernetes.io/docs/concepts/security/)
- [Kubernetes security checklist](https://kubernetes.io/docs/concepts/security/security-checklist/)
- [Pod Security Standards](https://kubernetes.io/docs/concepts/security/pod-security-standards/)
- [Using RBAC authorization](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)
- [Auditing](https://kubernetes.io/docs/tasks/debug/debug-cluster/audit/)
- [CNCF Cloud Native Security Whitepaper (TAG Security)](https://github.com/cncf/tag-security/tree/main/community/resources/security-whitepaper)
- [NIST SP 800-190: Application Container Security Guide](https://csrc.nist.gov/pubs/sp/800/190/final)
- [CIS Kubernetes Benchmark](https://www.cisecurity.org/benchmark/kubernetes)
- [Sigstore / Cosign docs](https://docs.sigstore.dev/), [Falco docs](https://falco.org/docs/), [Trivy docs](https://trivy.dev/), [Kyverno docs](https://kyverno.io/docs/)

## Focus list

- 4Cs of cloud native security, defense in depth, least privilege, zero trust
- API server flags, kubelet hardening, etcd protection, admission control
- Pod Security Standards, RBAC, NetworkPolicy, seccomp, capabilities
- STRIDE, common attack paths, supply chain attacks
- Image signing, scanning, SBOM, policy engines, service mesh mTLS
- CIS Benchmark, kube-bench, NIST SP 800-190, NSA/CISA hardening guide

## Files

- [practice-questions.md](practice-questions.md): 60 questions with answer key and explanations
- [mock-exams.md](mock-exams.md): two 15-question mocks

## Milestone

Both mocks at 80%+, then sit KCSA.
