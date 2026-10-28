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

## Files

- [practice-tasks.md](practice-tasks.md): 60 hands-on tasks with solutions
- [mock-exams.md](mock-exams.md): two 10-task mocks

## Milestone

Both mocks completed, then sit CKAD.
