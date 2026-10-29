# Module 3: CKAD (Certified Kubernetes Application Developer)

**Duration:** 13 weeks (weeks 12-24, months 3-6): a 4-week gap, 6 weeks of study, 3 weeks for the retake | **Previous:** [CKA](../02-cka/) | **Next:** [Module 4: KCSA](../04-kcsa/)

## Exam facts

| | |
|---|---|
| Format | Hands-on terminal tasks, ~15-20 tasks |
| Time | 2 hours |
| Pass mark | ~66% |
| Resources | kubernetes.io docs, Helm docs |

## Domains (approximate weights)

| Domain | Weight | Practice tasks |
|--------|--------|----------------|
| Application Environment, Configuration & Security | 25% | 34-48 |
| Application Design & Build | 20% | 1-12 |
| Application Deployment | 20% | 13-24 |
| Services & Networking | 20% | 49-60 |
| Application Observability & Maintenance | 15% | 25-33 |

## Plan

You already know the cluster from CKA, so this module is about speed with application YAML. CKAD took me two attempts, so it gets a 1-month gap before it and a retake window after it.

| Weeks | Focus |
|-------|-------|
| 12-15 (gap) | One month of extra preparation: imperative-command speed drills, `kubectl explain`, weak areas from CKA |
| 16 | Design and build: Pods, Jobs, CronJobs, multi-container Pods, image builds |
| 17 | Deployment: rollouts, canary, blue/green, Helm, Kustomize |
| 18 | Config and security: ConfigMaps, Secrets, securityContext, quotas, CRDs |
| 19 | Services, Ingress, NetworkPolicy |
| 20 | Probes, observability, debugging |
| 21 | Timed mocks, review every miss, first exam attempt |
| 22-24 | Retake window: review the domains you scored lowest in, then retake |

## Learning path

**KodeKloud courses (in this order)**

1. [Certified Kubernetes Application Developer (CKAD)](https://learn.kodekloud.com/learn/courses/certified-kubernetes-application-developer-ckad)
2. [Ultimate CKAD Mock Exam Series](https://learn.kodekloud.com/learn/courses/ultimate-certified-kubernetes-application-developer-ckad-mock-exam-series)

**Official and public resources**

- [CKAD exam page (Linux Foundation)](https://training.linuxfoundation.org/certification/certified-kubernetes-application-developer-ckad/) and [CNCF certification page](https://www.cncf.io/training/certification/ckad/)
- [Official CKAD curriculum](https://github.com/cncf/curriculum): use the CKAD PDF to check domains and weights
- [Exam tips for CKA and CKAD (Linux Foundation)](https://docs.linuxfoundation.org/tc-docs/certification/tips-cka-and-ckad)
- [kubectl quick reference](https://kubernetes.io/docs/reference/kubectl/quick-reference/)
- [Workloads: Pods, Deployments, Jobs, CronJobs](https://kubernetes.io/docs/concepts/workloads/)
- [Configuration: ConfigMaps, Secrets, resource management](https://kubernetes.io/docs/concepts/configuration/)
- [Configure liveness, readiness and startup probes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)
- [Configure a security context for a Pod or container](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)
- [Services, Ingress and NetworkPolicy](https://kubernetes.io/docs/concepts/services-networking/)
- [Custom Resources](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/)
- [Helm docs](https://helm.sh/docs/) and [Kustomize docs](https://kubectl.docs.kubernetes.io/)

## Files

- [practice-tasks.md](practice-tasks.md): 60 hands-on tasks with solutions
- [mock-exams.md](mock-exams.md): two 10-task mocks

## Milestone

Both mocks completed, then sit CKAD.
