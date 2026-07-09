# China Interview Preparation Workflow

You are preparing interview material for a China-market role.

## Step 0: Parse Input

`$ARGUMENTS` should contain:

```text
interview <job-file-or-evaluation>
```

If the path is missing or invalid, ask the user for a job file under
`markets/china/jobs/inbox/` or an evaluation file under `markets/china/jobs/evaluated/`.

## Step 1: Read Inputs

Read:

- The job or evaluation file.
- `documents/china/profile/candidate.md`
- `documents/china/profile/preferences.md`
- `documents/china/profile/evidence.md`
- `markets/china/templates/interview-answer.md`

If an application pack exists for the same company/role, read it for positioning
consistency.

## Step 2: Identify Interview Themes

Extract:

- Core technical or professional questions.
- Project deep-dive topics.
- Business/domain questions.
- Collaboration and communication questions.
- Motivation and stability questions.
- Salary, city, work mode, and offer-risk topics.

## Step 3: Build Answer Outlines

For each important question, provide:

- What the interviewer is testing.
- Evidence-backed answer angle.
- STAR or CAR outline.
- Metrics or facts to mention.
- What not to overclaim.

Use `documents/china/profile/evidence.md` as the source of truth.

## Step 4: Prepare Questions To Ask

Suggest questions about:

- Team responsibilities.
- Success metrics for the role.
- Reporting line and collaboration model.
- Product/business priorities.
- Onboarding expectations.
- Compensation structure if appropriate for the interview stage.

## Step 5: Write Prep File

Write `markets/china/jobs/evaluated/<slug>-interview.md`:

```markdown
# Interview Prep: <Role> @ <Company>

**Source:** <input file>
**Date:** YYYY-MM-DD

## Positioning

...

## Likely Questions And Answer Outlines

...

## Project Deep Dives

...

## Questions To Ask

...

## Risk Topics

...

## Salary / Offer Conversation Notes

...
```

## Step 6: Present Result

Summarize the most important preparation points and mention the output file path.
