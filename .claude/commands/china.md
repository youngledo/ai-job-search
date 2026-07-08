# /china - China Job Search Overlay

You are running the China-market overlay for this job-search workspace.

This command is intentionally a thin router. Do not duplicate the workflow
instructions here. Read the matching file under `markets/china/workflows/` and follow it
exactly.

## Supported Actions

Parse `$ARGUMENTS` as:

```text
<action> [path]
```

Actions:

- `setup` -> read and follow `markets/china/workflows/setup-profile.md`
- `analyze <job-file>` -> read and follow `markets/china/workflows/analyze-job.md`
- `apply <job-file>` -> read and follow `markets/china/workflows/apply-job.md`
- `rank` -> read and follow `markets/china/workflows/rank-jobs.md`
- `interview <job-file-or-evaluation>` -> read and follow `markets/china/workflows/interview-prep.md`

## Guardrails

- Do not scrape, log in to, message through, or automate BOSS Zhipin, Liepin,
  Zhaopin, 51job, Maimai, LinkedIn, or any other job platform.
- Use only manually saved job descriptions under `markets/china/jobs/inbox/`,
  user-pasted text, or files the user explicitly points to.
- Treat `markets/china/profile/evidence.md` and the profile files as the source
  of truth. Do not invent experience, credentials, skills, salary history, or
  project outcomes.
- Keep China-specific outputs under `markets/china/` unless the user explicitly asks to
  update the shared `job_search_tracker.csv`.

## Unknown Or Missing Action

If the action is missing or unknown, show this concise help:

```text
/china setup
/china analyze markets/china/jobs/inbox/<job>.md
/china apply markets/china/jobs/inbox/<job>.md
/china rank
/china interview markets/china/jobs/evaluated/<job>.md
```
