---
name: new-resume
description: >-
  Build a new resume from scratch by interviewing the candidate, filling every
  file under `resources/`, and generating a RenderCV-compatible YAML CV. Use
  when starting a resume with no existing source, importing a resume pasted into
  `from_existing.md`, bootstrapping the `resources/` evidence files, or when the
  user asks to build, create, or set up a resume or CV, or to be interviewed
  about their background to build one.
argument-hint: 'Optional: paste an existing resume into from_existing.md first.'
---

# New Resume

## Purpose

Turn a candidate and an optional pasted resume into a complete, truthful resume file set: every file under `./resources/` filled in, and a RenderCV YAML CV that renders cleanly. This is the intake skill — it runs before `resume-tailoring`. Nothing enters any file that the candidate has not supplied or confirmed.

## Inputs

- `./from_existing.md` — optional seed: a pasted existing resume, or empty.
- `./resources/` — the evidence files this skill fills (schemas below).
- `./.agents/skills/rendercv/SKILL.md` — RenderCV schema and rendering rules.
- `./.agents/AGENTS.md` — repository constraints.

## Resource Files

Fill each file from interview answers. Preserve the candidate's exact wording, numbers, employers, locations, and dates.

| File | Holds | Format |
|---|---|---|
| `resources/education.md` | Verified education facts | `- **Institution:** …`, `Area`, `Degree`, `Location` |
| `resources/experience.md` | Per employer: company, role, start, end, skills, description bullets | `## Company — Role` heading, bullet list |
| `resources/projects.md` | Resume-ready project bullets; deep dives live elsewhere | `## Project Name` heading, bullets |
| `resources/skills.md` | Flat list of technologies and capabilities | one `- ` bullet each |
| `resources/key_achievements.md` | High-level, quantified achievements | one `- ` bullet each |
| `resources/enhancers.md` | Soft skills and traits that complement the resume | one `- ` bullet each |
| `resources/<project>.md` | Optional per-project deep dive: problem, architecture, contribution, outcomes, scale | prose plus headings |
| `resources/performance_reviews.md` | Optional raw review material to mine into achievements and enhancers | pasted text |

`enhancers` is never its own resume section — blend it into summary, experience, or skills only. Always produce `education.md`; `resume-tailoring` depends on it.

## Procedure

### 1. Resolve the starting point

Read `./from_existing.md`.

- **Holds a resume** — extract every fact into a working gap list and pre-fill the resource files with it. Mark any inferred values.
- **Empty or placeholder only** — ask the candidate to either paste an existing resume into `from_existing.md` or start from scratch, and wait for the answer.

Then read anything already under `./resources/` so you extend it instead of overwriting the candidate's material.

### 2. Grill the candidate

Interview relentlessly until every resource file is complete and every claim is sourced. Model the missing facts as a design tree and work it in rounds.

- The **frontier** is every question whose prerequisites are already answered. Ask the whole frontier in one round, numbered. Then wait.
- Typical tree order: identity and contact → education → the employer list (company, role, dates, location) → per-employer highlights → projects → skills → achievements → enhancers.
- Where `from_existing.md` or an earlier answer lets you propose a concrete answer — a headline, a date, a metric — offer it as your recommendation to confirm or correct. For open questions with no derivable answer, just ask; never fabricate one.
- One topic per question. Follow up on scale, metrics, timing, and outcomes before accepting an answer: "improved reporting" is not a fact, "cut manual processing 90%" is.
- Recompute the frontier after each round. A question that depends on another still open this round waits for a later round.

Completion: no resource file has a blank field, and every bullet traces to the candidate or `from_existing.md`.

### 3. Write the resource files

Write each file in the schema above using the candidate's own words and figures. Keep one source of truth per fact. Put resume-ready project bullets in `projects.md`; push the full story into a `<project>.md` deep dive.

### 4. Generate the CV

Scaffold with `rendercv new "<Full Name>"`, then fill the `cv` section:

- `cv.name`, `headline`, `location`, and contact fields from the interview.
- `Summary` — 3–4 role-neutral, evidence-based statements.
- `experience`, `Skills`, `projects`, `Education`.

Keep the theme and rendering settings the scaffold provides unless the candidate asks otherwise. Quote any YAML string containing a colon.

### 5. Validate and render

Run diagnostics, render with the local RenderCV command, confirm PDF, HTML, Markdown, Typst, and PNG generation succeeds, and inspect the output for page count, clipped text, and layout. Aim for two pages or fewer. Fix only supported YAML or design settings; never edit generated files by hand.

## Rules

- Never invent experience, technologies, employers, dates, or metrics.
- Ask; do not assume — a blank answer stays out of the resume.
- Do not add an `Enhancers:` section.
- Phone numbers in E.164 international format; omit if unclear.
- Preserve the candidate's phrasing where it is already resume-ready.

## Completion Checklist

- Every file under `resources/` is filled from confirmed facts.
- No field left as a placeholder.
- `<Name>_CV.yaml` exists, validates, and renders.
- Every claim in the YAML traces to a resource file.
- The rendered PDF is selectable and preferably two pages or fewer.

## Example Prompts

- "Help me build a resume from scratch."
- "I pasted my old resume into `from_existing.md` — set up my resume repo."
- "Interview me and fill in the resources so I can start tailoring."
