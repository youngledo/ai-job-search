# China Profile Setup Workflow

You are setting up the China-market overlay profile.

There are two parallel locations involved — keeping them separate is what
prevents personal data from being committed to a public repo:

- `markets/china/profile/` — **templates**, tracked in git. Read-only for end
  users. They define the structure (section headings, China-specific fields
  like 薪资口径 / 五险一金 / 试用期 / 不接受外包) and serve as the starting point.
- `documents/china/profile/` — **your personal data**, gitignored via
  `documents/*/profile/**`. This is where the user's actual candidate,
  preferences, and evidence live.

**Never edit files under `markets/china/profile/`. Only edit files under
`documents/china/profile/`.** If you find yourself wanting to change a template
section heading or add a new field, that is a framework change — discuss it
with the user as such, do not silently mutate the template.

## Step 1: Initialize Personal Copies (First Run)

If `documents/china/profile/candidate.md` does not exist yet, seed the personal
copies from the templates:

```bash
mkdir -p documents/china/profile
cp markets/china/profile/candidate.md   documents/china/profile/candidate.md
cp markets/china/profile/preferences.md documents/china/profile/preferences.md
cp markets/china/profile/evidence.md    documents/china/profile/evidence.md
```

If the personal copies already exist, skip the `cp` step.

## Step 2: Read Current State

Read these personal files once:

- `documents/china/profile/candidate.md`
- `documents/china/profile/preferences.md`
- `documents/china/profile/evidence.md`

Also read `CLAUDE.md` and `.claude/skills/job-application-assistant/01-candidate-profile.md`
if they contain populated profile data. Use them as references, not as files to
edit.

## Step 3: Detect Gaps

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

1. Reading source documents from `documents/` (e.g., CV PDFs, LinkedIn exports).
2. Importing a pasted CV.
3. Running a short interview.

## Step 4: Build Or Update Profile

When the user provides information, update only the personal files:

- `documents/china/profile/candidate.md`
- `documents/china/profile/preferences.md`
- `documents/china/profile/evidence.md`

Keep Chinese market wording practical and specific. Do not add claims that the
user has not supplied or that are not supported by source material.

## Step 5: Cross-Check

Before finishing, verify:

- Candidate identity and contact details are consistent.
- Target roles and hard exclusions are present.
- Salary expectations are either filled in or explicitly marked as undecided.
- Work schedule, social insurance, probation, outsourcing / labor dispatch, and
  availability preferences are either filled in or explicitly marked as undecided.
- Every major claimed strength has evidence.
- Unsupported claims are moved to `需要补充证据的内容` or `不应声称的内容`.

## Step 6: Present Summary

Report:

- What was updated.
- What evidence-backed selling points are strongest.
- What information is still missing.
- Which command to run next, usually `/china analyze markets/china/jobs/inbox/<job>.md`.

Remind the user that personal files under `documents/china/profile/` are
gitignored — they will not appear in `git status` and will not be committed.
