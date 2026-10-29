# Module 2: CKA (Certified Kubernetes Administrator)

**Duration:** 8 weeks (weeks 4-11, months 1-3) | **Previous:** [KCNA](../01-kcna/) | **Next:** [Module 3: CKAD](../03-ckad/)

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

Follow the weekly rhythm in [study-method.md](../../docs/study-method.md). A suggested split of the 8 weeks:

| Week | Focus |
|------|-------|
| 1 | Cluster architecture, RBAC, kubeadm install and upgrade |
| 2 | etcd backup/restore, certificates |
| 3 | Helm, Kustomize, CRDs |
| 4 | Workloads and scheduling: taints, affinity, resources, static pods |
| 5 | Services, Ingress, Gateway API, NetworkPolicy, CoreDNS |
| 6 | Storage |
| 7 | Troubleshooting (nodes, control plane, networking) |
| 8 | Timed mocks, review every miss |

## Learning path

**KodeKloud courses (in this order)**

1. [Certified Kubernetes Administrator (CKA)](https://learn.kodekloud.com/learn/courses/cka-certification-course-certified-kubernetes-administrator)
2. [Ultimate CKA Mock Exam Series](https://learn.kodekloud.com/learn/courses/ultimate-certified-kubernetes-administrator-cka-mock-exam-series)

**Official and public resources**

- [CKA exam page (Linux Foundation)](https://training.linuxfoundation.org/certification/certified-kubernetes-administrator-cka/) and [CNCF certification page](https://www.cncf.io/training/certification/cka/)
- [Official CKA curriculum](https://github.com/cncf/curriculum): use the CKA PDF to check domains and weights
- [Exam tips for CKA and CKAD (Linux Foundation)](https://docs.linuxfoundation.org/tc-docs/certification/tips-cka-and-ckad)
- [kubectl quick reference](https://kubernetes.io/docs/reference/kubectl/quick-reference/)
- [Upgrading kubeadm clusters](https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/)
- [Operating etcd clusters (backup and restore)](https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/)
- [Using RBAC authorization](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)
- [Scheduling: taints, tolerations and affinity](https://kubernetes.io/docs/concepts/scheduling-eviction/)
- [Services, load balancing and networking](https://kubernetes.io/docs/concepts/services-networking/), [Gateway API](https://gateway-api.sigs.k8s.io/)
- [Storage: volumes, PV, PVC, StorageClass](https://kubernetes.io/docs/concepts/storage/)
- [Troubleshooting clusters](https://kubernetes.io/docs/tasks/debug/)
- [Helm docs](https://helm.sh/docs/) and [Kustomize docs](https://kubectl.docs.kubernetes.io/)

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
