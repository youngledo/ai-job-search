# China Job Application Workflow

You are creating China-market application material for a manually saved job
description. Do not contact the employer or operate any job platform.

## Step 0: Parse Input

`$ARGUMENTS` should contain:

```text
apply <job-file>
```

If the path is missing or invalid, stop and ask for a valid job file under
`markets/china/jobs/inbox/`.

## Step 1: Read Inputs

Read:

- The job file.
- `markets/china/profile/candidate.md`
- `markets/china/profile/preferences.md`
- `markets/china/profile/evidence.md`
- `markets/china/templates/boss-greeting.md`
- `markets/china/templates/recruiter-message.md`
- `markets/china/templates/chinese-cover-letter.md`
- `markets/china/templates/interview-answer.md`
- `cv/chinese/main_example.tex`
- `cover_letters/chinese/cover_example.tex`

If an evaluation exists under `markets/china/jobs/evaluated/` for the same company/role,
read it and use its score, strengths, gaps, and red flags.

## Step 2: Factual Guard

Before drafting, identify:

- Claims that are fully supported by evidence.
- Claims that are plausible but need user confirmation.
- Gaps that must remain visible.

Do not write unsupported claims as facts. If the job asks for a missing skill,
phrase it as a learning/adjacent-experience angle only when honest.

## Step 3: Draft Outputs

Produce:

- BOSS 直聘打招呼话术: 1 concise version under 80 Chinese characters, plus 1
  slightly fuller version under 140 Chinese characters.
- 招聘者/猎头私信: one message suitable for Maimai, WeChat, or email.
- 中文求职信/邮件: concise, role-specific, evidence-backed.
- 简历修改建议: bullets to emphasize, bullets to remove, keywords to add only if
  evidence supports them.
- 中文 LaTeX 简历/求职信生成建议: if the user explicitly asks for full `.tex`
  files, use `cv/chinese/main_example.tex` and
  `cover_letters/chinese/cover_example.tex` as structural references. Otherwise,
  keep the output as targeted resume-editing guidance and a concise letter/email.
- 面试准备重点: likely questions and evidence-backed answer angles.

Tone:

- Specific, direct, and professional.
- Avoid exaggerated slogans such as "我对贵司仰慕已久" unless the user provides a
  concrete reason.
- Avoid pretending to have experience the profile does not support.

## Step 4: Save Application Pack

Write `markets/china/jobs/evaluated/<slug>-application.md`:

```markdown
# Application Pack: <Role> @ <Company>

**Source:** <job file>
**Date:** YYYY-MM-DD

## Supported Positioning

...

## BOSS Greeting

...

## Recruiter Message

...

## Chinese Cover Letter / Email

...

## Resume Tailoring Suggestions

...

## Chinese LaTeX Template Notes

Use `cv/chinese/main_example.tex` and `cover_letters/chinese/cover_example.tex`
only if the user asks for full compilable documents. Keep all generated personal
files out of git-tracked template paths.

## Interview Focus

...

## Gaps To Keep Honest

...

## User Confirmation Needed

...
```

## Step 5: Present Result

Show the BOSS greeting, recruiter message, and output file path. Keep the summary
short and mention any user confirmations needed before sending.
