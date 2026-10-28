# Kubestronaut in 6 Months: A Short-Term Course

A self-paced, hands-on course for earning all five Kubernetes certifications that make you a **Kubestronaut**: **KCNA, KCSA, CKA, CKAD and CKS**. It is built from my own journey and bundles a 6-month study plan, 300 practice questions and tasks, and 10 mock exams that you can reuse.

> Unofficial community material. It is practice content, not real exam questions or "dumps". Always check prices, pass marks, domain weights and the exam version on the official [Linux Foundation / CNCF](https://training.linuxfoundation.org/certification/kubernetes-cloud-native-associate/) pages and the [CNCF curriculum repo](https://github.com/cncf/curriculum) before you book.

## What you get

| | |
|---|---|
| 6-month plan | Week-by-week schedule, ordered so CKA comes before CKS |
| 300 practice items | 60 per certification: 120 multiple-choice questions and 180 hands-on tasks with solutions |
| 10 mock exams | Two per certification (diagnostic + dress rehearsal) |
| Study method | Weekly rhythm, mock routine, exam-day checklist |
| Tracker | Mock scores, exam dates and expiry dates in one table |

## Course modules

Follow the modules in this order. Each folder has its own README with exam facts, domains, a focus list and a milestone.

| # | Module | Exam | Weeks | Practice bank | Mocks |
|---|--------|------|-------|---------------|-------|
| 1 | [KCNA](certifications/01-kcna/) Kubernetes and Cloud Native Associate | 60 MCQ, 90 min | 2 | [60 questions](certifications/01-kcna/practice-questions.md) | [2 mocks](certifications/01-kcna/mock-exams.md) |
| 2 | [CKA](certifications/02-cka/) Certified Kubernetes Administrator | Hands-on, 2 h | 6 | [60 tasks](certifications/02-cka/practice-tasks.md) | [2 mocks](certifications/02-cka/mock-exams.md) |
| 3 | [CKAD](certifications/03-ckad/) Certified Kubernetes Application Developer | Hands-on, 2 h | 5 | [60 tasks](certifications/03-ckad/practice-tasks.md) | [2 mocks](certifications/03-ckad/mock-exams.md) |
| 4 | [KCSA](certifications/04-kcsa/) Kubernetes and Cloud Native Security Associate | 60 MCQ, 90 min | 2 | [60 questions](certifications/04-kcsa/practice-questions.md) | [2 mocks](certifications/04-kcsa/mock-exams.md) |
| 5 | [CKS](certifications/05-cks/) Certified Kubernetes Security Specialist | Hands-on, 2 h | 8 | [60 tasks](certifications/05-cks/practice-tasks.md) | [2 mocks](certifications/05-cks/mock-exams.md) |
| 6 | Buffer: retakes, gap review, claim Kubestronaut | | 3 | | |

Total: about 26 weeks at 8-10 hours per week. See the full [study plan](docs/study-plan.md).

## Repository layout

```
Skommepalli_Kubestronaut/
├── README.md                     <- you are here
├── certifications/
│   ├── 01-kcna/                  README + practice-questions + mock-exams
│   ├── 02-cka/                   README + practice-tasks + mock-exams
│   ├── 03-ckad/                  README + practice-tasks + mock-exams
│   ├── 04-kcsa/                  README + practice-questions + mock-exams
│   └── 05-cks/                   README + practice-tasks + mock-exams
├── docs/
│   ├── study-plan.md             6-month schedule and program rules
│   ├── study-method.md           weekly rhythm, mock routine, exam-day checklist
│   ├── resources.md              courses, repos and official links
│   └── linkedin-post.md          the story behind this repo, ready to post
└── tracker/
    └── progress-tracker.md       mock scores, exam dates, expiry dates
```

## How to use this course

1. Read the [program rules](docs/study-plan.md#program-rules-that-affect-planning). CKS needs an active CKA, and all five certs must be valid at the same time.
2. Work through one module at a time, in order. Start with the module README.
3. Study the curriculum domains, then drill the practice bank for that certification.
4. Take **Mock 1** as a diagnostic about 7-10 days before the exam, study only the weak domains, then take **Mock 2** under exam conditions.
5. Book the exam only when Mock 2 passes comfortably.
6. Log everything in the [tracker](tracker/progress-tracker.md) and write a one-line review for each miss (see [study method](docs/study-method.md)).

## Prerequisites

- Basic Linux command line and YAML.
- A practice cluster for the hands-on exams: kind, minikube, kubeadm on VMs, or a hosted lab such as KodeKloud or Killercoda.
- Time: roughly 8-10 hours per week.

## Resources

### Official

* CNCF curriculum PDFs for every exam: https://github.com/cncf/curriculum
* Linux Foundation certification pages and candidate handbooks: https://training.linuxfoundation.org
* Kubernetes documentation (allowed in the hands-on exams): https://kubernetes.io/docs

### KodeKloud Kubestronaut learning path (used in this journey)

1. [Kubernetes for the Absolute Beginners - Hands-on Tutorial](https://learn.kodekloud.com/learn/courses/kubernetes-for-the-absolute-beginners-hands-on-tutorial)
2. [Kubernetes and Cloud-Native Associate (KCNA)](https://learn.kodekloud.com/learn/courses/kubernetes-and-cloud-native-associate-kcna)
3. [Certified Kubernetes Administrator (CKA)](https://learn.kodekloud.com/learn/courses/cka-certification-course-certified-kubernetes-administrator)
4. [Ultimate CKA Mock Exam Series](https://learn.kodekloud.com/learn/courses/ultimate-certified-kubernetes-administrator-cka-mock-exam-series)
5. [Certified Kubernetes Application Developer (CKAD)](https://learn.kodekloud.com/learn/courses/certified-kubernetes-application-developer-ckad)
6. [Ultimate CKAD Mock Exam Series](https://learn.kodekloud.com/learn/courses/ultimate-certified-kubernetes-application-developer-ckad-mock-exam-series)
7. [Kubernetes and Cloud Native Security Associate (KCSA)](https://learn.kodekloud.com/learn/courses/kubernetes-and-cloud-native-security-associate-kcsa)
8. [Certified Kubernetes Security Specialist (CKS)](https://learn.kodekloud.com/learn/courses/certified-kubernetes-security-specialist-cks)
9. [CKS - Challenges](https://learn.kodekloud.com/learn/courses/cks-challenges)

### Community

* CNCF Certification Notes: https://github.com/rashidwassan/CNCF-Certification-Notes

### About the practice material in this repo

The practice banks and mock exams were drafted with AI assistance (Claude) and checked against the curriculum. They are original practice content, not real exam questions. If you find a mistake, please open an issue.

## Contributing

Found a wrong answer, an outdated flag or a new Kubernetes version change? Open an issue or a pull request. Corrections are very welcome.

## Author

Seshadri Kommepalli ([@skommepa](https://github.com/skommepa)).
