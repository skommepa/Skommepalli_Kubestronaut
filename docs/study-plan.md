# Six-Month Study Plan

Plan window: **27 Oct 2026 to about 26 Apr 2027**, assuming 8-10 hours per week. Shift blocks if a holiday or a work peak hits. The order respects the rule that CKS needs a current CKA.

> Verify prices, passing scores, domain weights and the Kubernetes exam version on the official Linux Foundation / CNCF pages before booking. They change between releases.

## Program rules that affect planning

- **Kubestronaut** means holding all five certifications active at the same time: KCNA, KCSA, CKA, CKAD, CKS.
- **CKS requires a current CKA.** Do CKA before CKS.
- The later you sit your first exam, the less margin you have, so book all exams within the same 6-month window and note each expiry date.
- Exam purchases normally include one free retake. Treat it as insurance, not as part of the plan.
- Bundles exist (individual exams vs. the Kubestronaut bundle). Compare prices at checkout.

## Timeline

| Phase | Dates | Weeks | Module | Milestone |
|-------|-------|-------|--------|-----------|
| 1 | 27 Oct - 9 Nov | 2 | [KCNA](../certifications/01-kcna/) | Both KCNA mocks at 80%+, then sit KCNA |
| 2 | 10 Nov - 21 Dec | 6 | [CKA](../certifications/02-cka/) | Both CKA mocks completed in under 2 h, then sit CKA |
| 3 | 22 Dec - 25 Jan | 5 | [CKAD](../certifications/03-ckad/) | Both CKAD mocks completed, then sit CKAD |
| 4 | 26 Jan - 8 Feb | 2 | [KCSA](../certifications/04-kcsa/) | Both KCSA mocks at 80%+, then sit KCSA |
| 5 | 9 Feb - 5 Apr | 8 | [CKS](../certifications/05-cks/) | KodeKloud CKS challenges plus both CKS mocks, then sit CKS |
| 6 | 6 Apr - 26 Apr | 3 | Buffer | Retake slot if needed, re-certify gaps, claim Kubestronaut |

## Why this order

- **KCNA first** is a gentle start that builds vocabulary for everything else.
- **CKA before CKAD** because administration (cluster, networking, troubleshooting) gives the foundation that application work builds on.
- **KCSA right before CKS** so the security concepts are fresh when you do the hands-on security exam.
- **CKS last** because it is the hardest and needs a valid CKA.
- **A 3-week buffer** protects you from a retake or a delayed exam slot.

## Exam patterns at a glance

| Exam | Type | Duration | Questions | Typical pass mark | Open resources |
|------|------|----------|-----------|-------------------|----------------|
| KCNA | Multiple choice, online proctored | 90 min | ~60 | ~75% | None |
| KCSA | Multiple choice, online proctored | 90 min | ~60 | ~75% | None |
| CKA | Hands-on terminal tasks | 2 h | ~15-20 tasks | ~66% | kubernetes.io docs, GitHub k8s, Helm docs |
| CKAD | Hands-on terminal tasks | 2 h | ~15-20 tasks | ~66% | kubernetes.io docs, Helm docs |
| CKS | Hands-on terminal tasks | 2 h | ~15-20 tasks | ~67% | kubernetes.io docs plus tool docs (Trivy, Falco, AppArmor) |

## Weekly rhythm

The full rhythm and the two-mock routine are in [study-method.md](study-method.md). In short:

- **Hands-on exams (CKA, CKAD, CKS):** Mon-Tue one domain, Wed timed drills, Thu troubleshooting, Sat full timed mock, Sun rest.
- **Multiple-choice exams (KCNA, KCSA):** 45-60 minutes daily on a curriculum topic plus 15-20 practice questions; mock 1 at the end of week 1 and mock 2 at the end of week 2.
