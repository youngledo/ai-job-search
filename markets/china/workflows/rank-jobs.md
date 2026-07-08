# China Job Ranking Workflow

You are ranking manually saved China-market job descriptions. Do not fetch,
scrape, log in to, or automate any job platform.

## Step 1: Load Jobs

Find Markdown files under `markets/china/jobs/inbox/`.

If none exist, tell the user to save job descriptions as:

```text
markets/china/jobs/inbox/<company>-<role>.md
```

Skip files that are too thin to evaluate, such as files with only a title and no
responsibilities or requirements.

## Step 2: Load Profile

Read:

- `markets/china/profile/candidate.md`
- `markets/china/profile/preferences.md`
- `markets/china/profile/evidence.md`

If the profile is too sparse, stop and ask the user to run `/china setup`.

## Step 3: Score Each Job

Use the same scoring dimensions and weights as `markets/china/workflows/analyze-job.md`:

- Technical match: 25%.
- Experience match: 25%.
- Domain match: 15%.
- Communication fit: 10%.
- Compensation/location fit: 10%.
- Growth fit: 15%.

Apply hard vetoes for:

- City/work mode outside stated hard constraints.
- Salary clearly below minimum expectation.
- Required skill or credential that the candidate clearly lacks and cannot
  credibly bridge.
- Role type listed under `暂不考虑岗位`.

## Step 4: Write Ranking Report

Write `markets/china/jobs/evaluated/ranking-YYYY-MM-DD.md`:

```markdown
# China Job Ranking - YYYY-MM-DD

## Summary

Ranked <N> jobs. Skipped <M> jobs due to insufficient JD detail.

## Shortlist

| Rank | Score | Verdict | Company | Role | Location | Next Action |
|---:|---:|---|---|---|---|---|

## Why The Top Jobs Ranked Highest

...

## Below Threshold

...

## Vetoed / Skipped

...

## Assumptions / Missing Info

...
```

## Step 5: Present Result

Show the top five jobs, any vetoed jobs, and the report path. Remind the user
that `/china apply <job-file>` creates materials for a selected job.
