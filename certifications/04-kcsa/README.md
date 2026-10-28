# Module 4: KCSA (Kubernetes and Cloud Native Security Associate)

**Duration:** 2 weeks (26 Jan - 8 Feb) | **Previous:** [CKAD](../03-ckad/) | **Next:** [Module 5: CKS](../05-cks/)

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

- **Week 1:** 45-60 min a day on one domain plus 15-20 practice questions. Finish with [Mock 1](mock-exams.md).
- **Week 2:** Fix weak domains, then take Mock 2 and the full [60-question bank](practice-questions.md).

This module doubles as the concept primer for CKS, so take notes on the tools (Trivy, Falco, Cosign, Kyverno, Gatekeeper).

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
