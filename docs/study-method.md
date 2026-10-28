# Study Method

The weekly rhythm, mock-exam routine and exam-day checklist used throughout this course.

## Weekly rhythm for the hands-on exams (CKA, CKAD, CKS)
- Mon-Tue: one domain from the curriculum, doing every task from the docs with imperative commands.
- Wed: timed drills (10 small tasks in 30 min).
- Thu: troubleshooting or break-and-fix practice.
- Sat: full timed mock (2 h), then review every miss.
- Sun: rest or light flashcards.

## Weekly rhythm for KCNA and KCSA
- Daily 45-60 min: curriculum topic plus 15-20 practice questions.
- End of week 1: mock 1. End of week 2: mock 2. Review wrong answers against the curriculum PDF.

## Two mocks per certification: how to use them
1. Mock 1 about 7-10 days before the exam: diagnostic. Note weak domains.
2. Study the weak domains only for 4-5 days.
3. Mock 2 about 2-3 days before the exam: dress rehearsal with the exact conditions (time limit, docs only, no notes).
4. Book the exam only when mock 2 is passed comfortably.

## Exam-day checklist (hands-on exams)
- Set up at the start (about 2 minutes):
  `alias k=kubectl`, `export do="--dry-run=client -o yaml"`, `export now="--force --grace-period=0"`, kubectl bash completion, and in `.vimrc`: `set tabstop=2 shiftwidth=2 expandtab`.
- Switch context on every task (the command is given in the question).
- Skim all tasks first, do high-weight and easy ones first, flag the slow ones.
- Verify each answer (`k get`, `k describe`, `curl` from a test pod).
- Use `k explain <resource>.spec --recursive` and the docs search instead of memorising YAML.

## How to review a mock

For every miss, write one line:
`Task / question -> what I did -> what was right -> doc page to bookmark`

After two mocks per certification you will have 10-20 lines. Those lines are your final-day revision sheet.
