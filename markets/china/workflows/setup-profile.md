# China Profile Setup Workflow

You are setting up the China-market overlay profile. Only edit files under
`markets/china/profile/`.

## Step 1: Read Current State

Read these files once:

- `markets/china/profile/candidate.md`
- `markets/china/profile/preferences.md`
- `markets/china/profile/evidence.md`

Also read `CLAUDE.md` and `.claude/skills/job-application-assistant/01-candidate-profile.md`
if they contain populated profile data. Use them as references, not as files to
edit.

## Step 2: Detect Gaps

Check for:

- Empty profile sections.
- Placeholders that still need user input.
- Missing target roles, target cities, salary expectations, and hard exclusions.
- Missing China-market logistics: years of experience, availability, expected
  monthly salary and salary months, acceptable work schedule, social insurance
  requirements, probation limits, and whether outsourcing / labor dispatch is acceptable.
- Experience claims in `candidate.md` that do not have matching support in
  `evidence.md`.

If many sections are empty, ask the user whether to proceed by:

1. Reading source documents from `documents/`.
2. Importing a pasted CV.
3. Running a short interview.

## Step 3: Build Or Update Profile

When the user provides information, update only:

- `markets/china/profile/candidate.md`
- `markets/china/profile/preferences.md`
- `markets/china/profile/evidence.md`

Keep Chinese market wording practical and specific. Do not add claims that the
user has not supplied or that are not supported by source material.

## Step 4: Cross-Check

Before finishing, verify:

- Candidate identity and contact details are consistent.
- Target roles and hard exclusions are present.
- Salary expectations are either filled in or explicitly marked as undecided.
- Work schedule, social insurance, probation, outsourcing / labor dispatch, and
  availability preferences are either filled in or explicitly marked as undecided.
- Every major claimed strength has evidence.
- Unsupported claims are moved to `需要补充证据的内容` or `不应声称的内容`.

## Step 5: Present Summary

Report:

- What was updated.
- What evidence-backed selling points are strongest.
- What information is still missing.
- Which command to run next, usually `/china analyze markets/china/jobs/inbox/<job>.md`.
