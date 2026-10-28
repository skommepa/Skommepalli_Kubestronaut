# 10-Month Study Plan

This is the plan I actually followed: **about 10 months (43 weeks)** at 8-10 hours per week. It started as a 6-month plan, and I revised it many times. The two hardest hands-on exams, **CKAD and CKS, each got a 1-month gap of extra preparation**, and I failed each of them once and passed on the second attempt. The retake weeks are built into the schedule below so you don't have to squeeze them in.

> Verify prices, passing scores, domain weights and the Kubernetes exam version on the official Linux Foundation / CNCF pages before booking. They change between releases.

## Program rules that affect planning

- **Kubestronaut** means holding all five certifications active at the same time: KCNA, KCSA, CKA, CKAD, CKS.
- **CKS requires a current CKA.** Do CKA before CKS.
- Each certification has an expiry date, and all five must be valid together. Note each expiry date when you pass.
- Exam purchases normally include one free retake. In my case I needed it twice, so plan for it instead of hoping you won't.
- Bundles exist (individual exams vs. the Kubestronaut bundle). Compare prices at checkout.

## Timeline

| Phase | Weeks | Approx. month | Module | Milestone |
|-------|-------|---------------|--------|-----------|
| 1 | 1-3 | 1 | [KCNA](../certifications/01-kcna/) | Both KCNA mocks at 80%+, then sit KCNA |
| 2 | 4-11 | 1-3 | [CKA](../certifications/02-cka/) | Both CKA mocks completed in under 2 h, then sit CKA |
| 3a | 12-15 | 3-4 | **1-month gap** before CKAD | Extra preparation: speed drills, weak areas from CKA |
| 3b | 16-21 | 4-5 | [CKAD](../certifications/03-ckad/) | Both CKAD mocks completed, then sit CKAD |
| 3c | 22-24 | 6 | CKAD retake | Review every miss, retake CKAD (passed on 2nd attempt) |
| 4 | 25-27 | 6-7 | [KCSA](../certifications/04-kcsa/) | Both KCSA mocks at 80%+, then sit KCSA |
| 5a | 28-31 | 7-8 | **1-month gap** before CKS | Extra preparation: Falco, Trivy, AppArmor, audit logging |
| 5b | 32-40 | 8-10 | [CKS](../certifications/05-cks/) | KodeKloud CKS challenges plus both CKS mocks, then sit CKS |
| 5c | 41-43 | 10 | CKS retake | Review every miss, retake CKS (passed on 2nd attempt) |

Total: about 43 weeks, roughly 10 months. If you pass first time, you can skip the retake phases (3c and 5c) and finish about 6 weeks sooner. Month numbers are approximate. Shift blocks for holidays or work peaks.

## Why this order

- **KCNA first** is a gentle start that builds vocabulary for everything else.
- **CKA before CKAD** because administration (cluster, networking, troubleshooting) gives the foundation that application work builds on.
- **KCSA right before CKS** so the security concepts are fresh when you do the hands-on security exam.
- **CKS last** because it is the hardest and needs a valid CKA.
- **A 1-month gap before CKAD and before CKS.** These were the two exams that needed the most extra time for me. The gap is for speed drills, weak areas and extra lab hours, not for new theory.
- **Retake weeks after CKAD and CKS** so a failed first attempt doesn't wreck the rest of the schedule.

## Lessons from the retakes

- A pass mark of about 66% on the hands-on exams leaves little room. Speed matters as much as knowledge.
- Review every miss within a day and write one line for it (see [study-method.md](study-method.md)).
- After a failed attempt, spend the first week on the exact domains you scored lowest in, not on everything.
- Practise in an environment as close to the real exam as possible: only the allowed docs, a strict 2-hour timer.

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
- **Multiple-choice exams (KCNA, KCSA):** 45-60 minutes daily on a curriculum topic plus 15-20 practice questions; mock 1 and mock 2 in the final week.
