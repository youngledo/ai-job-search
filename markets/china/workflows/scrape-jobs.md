# China Job Scrape Workflow

You are searching for China-market job postings from public pages. This workflow
uses low-volume WebSearch and WebFetch only. Do not log in, use cookies, bypass
anti-bot systems, message recruiters, apply to jobs, or operate any platform
account.

## Step 0: Parse Input

`$ARGUMENTS` should contain:

```text
scrape [focus|broad]
```

- No focus: use the top target roles, cities, and industries from
  `documents/china/profile/preferences.md`.
- `focus`: prioritize that role, skill, industry, or city.
- `broad`: run more query categories, but keep volume low.

## Step 1: Read Inputs

Read:

- `documents/china/profile/preferences.md`
- `documents/china/profile/candidate.md`
- `markets/china/search-queries.md`
- `job_search_tracker.csv` if it exists
- `job_scraper/seen_jobs.json` if it exists; create it if missing with
  `{"seen": {}}`

Use target roles, cities, industries, hard exclusions, salary minimums, and work
mode preferences to build search terms.

## Step 2: Build Search Queries

Default public sources:

- BOSS Zhipin (`site:zhipin.com`)
- Liepin (`site:liepin.com`)
- Zhaopin (`site:zhaopin.com`)
- 51job (`site:51job.com`)
- Maimai (`site:maimai.cn`)
- Guopin (`site:iguopin.com`)
- Company career pages

Do not include LinkedIn by default for China-mainland searches. Only use LinkedIn
when the user explicitly asks for international, foreign-company, outbound, or
English-language roles.

Do not include discontinued or user-excluded job boards.

Generate a small set of targeted WebSearch queries:

- Default: up to 8 queries.
- Focus mode: up to 6 focused queries.
- Broad mode: up to 15 queries.

Prefer precise queries over broad scraping. Include city and role terms whenever
possible.

## Step 3: Search Public Results

Run WebSearch queries. For each promising result, keep:

- Title.
- URL.
- Search snippet.
- Source site.
- Apparent company and role if visible.

Skip results that are clearly expired, unrelated, outside hard location
constraints, or duplicates.

## Step 4: Fetch Public Pages

For promising results only, use WebFetch once per URL.

Classify each result:

- `ready`: full JD is publicly readable and includes enough responsibilities and
  requirements for evaluation.
- `manual_required`: result is relevant, but WebFetch returns a login page,
  anti-bot page, partial snippet, empty body, or otherwise incomplete JD.
- `blocked`: page explicitly blocks automated/public access.
- `duplicate`: URL or company+role already appears in `seen_jobs.json`,
  `job_search_tracker.csv`, or `markets/china/jobs/inbox/`.
- `skip`: unrelated, expired, outside constraints, or too weak to keep. Also
  applies when the JD explicitly requires education credentials the candidate
  does not have — see `documents/china/profile/preferences.md` "学历排除":
  - "全日制本科" (without "接受专升本" wording)
  - "统招本科" (meaning full-time unified enrollment, excluding 统招专升本)
  - "学士学位" (candidate has graduation certificate but no degree certificate)
  - "985/211 本科"
  - Record the trigger in the `seen_jobs.json` entry's `skip_reason` as
    `education_mismatch_<specific_wording>`, e.g.
    `education_mismatch_full_time_bachelor`,
    `education_mismatch_bachelor_degree_required`,
    `education_mismatch_985_211`.

Never infer missing responsibilities, requirements, salary, or benefits from the
title alone.

## Step 5: Save Job Files

For `ready` results, write:

```text
markets/china/jobs/inbox/<company>-<role>.md
```

Use this structure:

```markdown
# <Role> @ <Company>

**Source:** <site>
**Source URL:** <url>
**Fetch Status:** ready
**Saved Date:** YYYY-MM-DD

## Job Facts

- Company:
- Role:
- Location:
- Work Mode:
- Salary:
- Employment Type:

## Responsibilities

...

## Requirements

...

## Preferred Qualifications

...

## Benefits / Work Conditions

...

## Notes

- Search snippet:
- Missing info:
```

For `manual_required` or `blocked` results that look relevant, write:

```text
markets/china/jobs/inbox/<company>-<role>-manual-required.md
```

Use this structure:

```markdown
# <Role> @ <Company>

**Source:** <site>
**Source URL:** <url>
**Fetch Status:** manual_required
**Saved Date:** YYYY-MM-DD
**Manual Action Needed:** Open the source URL yourself and paste the full JD below.

## Search Snippet

...

## Paste Full JD Below

```

Add every kept URL to `job_scraper/seen_jobs.json` with:

```json
{
  "title": "...",
  "company": "...",
  "url": "...",
  "source": "...",
  "first_seen": "YYYY-MM-DD",
  "market": "china",
  "status": "ready/manual_required/blocked/duplicate/skipped"
}
```

## Step 6: Present Results

Present a concise table:

```markdown
## China Job Search Results - YYYY-MM-DD

| # | Status | Company | Role | Source | Location | File |
|---:|---|---|---|---|---|---|
```

Then show:

- Ready to analyze: files that can be passed to `/china analyze`.
- Manual required: files where the user must paste the full JD.
- Skipped/duplicates: count only, unless the user asks for details.

If no ready results are found, say whether the blocker was search quality,
platform blocking, sparse profile preferences, or too-strict filters. Suggest
either refining `documents/china/profile/preferences.md` or manually adding a JD.

## Important Rules

1. Do not log in, use cookies, bypass anti-bot systems, message recruiters, or
   apply to jobs.
2. Public search and single-page public fetch are allowed; platform operation is
   not.
3. Do not fabricate JD details. If content is incomplete, create a
   `manual_required` file.
4. Keep all China-market output under `markets/china/jobs/` unless the user
   explicitly asks to update `job_search_tracker.csv`.
5. Respect deduplication before presenting jobs.
