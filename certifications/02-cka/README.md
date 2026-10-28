# Module 2: CKA (Certified Kubernetes Administrator)

**Duration:** 6 weeks (10 Nov - 21 Dec) | **Previous:** [KCNA](../01-kcna/) | **Next:** [Module 3: CKAD](../03-ckad/)

## Exam facts

| | |
|---|---|
| Format | Hands-on terminal tasks, ~15-20 tasks |
| Time | 2 hours |
| Pass mark | ~66% |
| Resources | kubernetes.io docs, GitHub k8s, Helm docs |

## Domains (approximate weights)

| Domain | Weight | Practice tasks |
|--------|--------|----------------|
| Troubleshooting | 30% | 44-60 |
| Cluster Architecture, Installation & Configuration | 25% | 1-15 |
| Services & Networking | 20% | 26-37 |
| Workloads & Scheduling | 15% | 16-25 |
| Storage | 10% | 38-43 |

## Plan

Follow the weekly rhythm in [study-method.md](../../docs/study-method.md). A suggested split of the 6 weeks:

| Week | Focus |
|------|-------|
| 1 | Cluster architecture, RBAC, kubeadm install and upgrade |
| 2 | etcd backup/restore, certificates, Helm and Kustomize |
| 3 | Workloads and scheduling: taints, affinity, resources, static pods |
| 4 | Services, Ingress, Gateway API, NetworkPolicy, CoreDNS |
| 5 | Storage, then troubleshooting (nodes, control plane, networking) |
| 6 | Timed mocks, review every miss |

## Files

- [practice-tasks.md](practice-tasks.md): 60 hands-on tasks with solutions. Run as Set A (1-20), Set B (21-40), Set C (41-60), or mix 15-18 tasks.
- [mock-exams.md](mock-exams.md): two 10-task mocks

## Exam-day setup

```bash
alias k=kubectl
export do="--dry-run=client -o yaml"
export now="--force --grace-period=0"
```

## Milestone

Both mocks completed in under 2 hours, then sit CKA. Note the expiry date: CKS needs a current CKA.
