# China Job Analysis Workflow

You are evaluating a manually saved job description for the China-market overlay.
Do not fetch, scrape, log in to, or automate any job platform.

## Step 0: Parse Input

`$ARGUMENTS` should contain:

```text
analyze <job-file>
```

If the path is missing or the file does not exist, stop and ask the user to save
the JD under `markets/china/jobs/inbox/` or provide a valid path.

## Step 1: Read Inputs

Read:

- The job file.
- `markets/china/profile/candidate.md`
- `markets/china/profile/preferences.md`
- `markets/china/profile/evidence.md`

If profile files are still sparse, continue only if the job can be evaluated
honestly. Otherwise ask the user to run `/china setup` first.

## Step 2: Extract Job Facts

Extract, when present:

- Company.
- Role title.
- Platform/source.
- Location and work mode.
- Salary range, salary months, bonus structure, stock/options, and whether the
  figure is pre-tax.
- Department/team.
- Responsibilities.
- Required skills.
- Preferred skills.
- Experience level.
- Education/language requirements.
- Work schedule: standard 5-day, flexible, 996,大小周, on-call, frequent overtime.
- Employment type: direct hire, outsourcing, labor dispatch / 劳务派遣, contractor,
  internship, or unclear.
- Social insurance / 五险一金: full contribution, minimum-base contribution,
  unclear, or absent.
- Probation terms: length, probation salary, conversion criteria, and any unpaid
  trial-work signal.
- Application deadline.
- Red flags such as vague role scope, unpaid trial work, heavy overtime signals,
  unrealistic skill stack, outsourcing/dispatch ambiguity, abnormal probation,
  social-insurance ambiguity, or salary mismatch.

If facts are missing, list them under `Assumptions / Missing Info` instead of
guessing.

## Step 3: Score Fit

Score each dimension from 0 to 100:

- Technical match: required hard skills and tools.
- Experience match: role level, project depth, business ownership.
- Domain match: industry, customer type, product type, market familiarity.
- Communication fit: writing, stakeholder, sales, cross-team, or client-facing
  expectations.
- Compensation/location fit: salary range, salary months, tax basis, city,
  commute, remote/hybrid fit, social insurance, probation, and employment type.
- Growth fit: whether the role advances the user's target direction.

Overall score:

```text
technical 25% + experience 25% + domain 15% + communication 10% + compensation/location 10% + growth 15%
```

Verdict bands:

- 80-100: Strong fit, worth prioritizing.
- 65-79: Good fit, worth contacting if main constraints pass.
- 50-64: Moderate fit, proceed only if role/company is strategically valuable.
- 35-49: Weak fit, likely not worth active effort.
- 0-34: Poor fit, skip unless the user has a special reason.

## Step 4: Write Evaluation

Create `markets/china/jobs/evaluated/<slug>.md`, where `<slug>` is a lowercase
company-role slug derived from the job file name or extracted facts.

Use this structure:

```markdown
# Job Evaluation: <Role> @ <Company>

**Source:** <job file>
**Date:** YYYY-MM-DD
**Verdict:** <band>
**Overall Score:** <score>/100

## Job Facts

...

## Scorecard

| Dimension | Score | Evidence |
|---|---:|---|

## Strengths

- ...

## Gaps

- ...

## Red Flags

- ...

## China-Market Checks

| Check | Finding | Risk |
|---|---|---|
| Salary package | ... | ... |
| Work schedule | ... | ... |
| Social insurance / 五险一金 | ... | ... |
| Probation / 试用期 | ... | ... |
| Employment type | ... | ... |

## Recommended Next Action

...

## BOSS / Recruiter Angle

...

## Assumptions / Missing Info

- ...
```

## Step 5: Present Result

Summarize the verdict, top three strengths, top three gaps, and next action.
Mention the output file path.
