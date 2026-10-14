---
name: resume-tailoring
description: 'Create and tailor a truthful, ATS-friendly RenderCV resume from a job description, and judge whether the current resume passes the ATS screen. Use when adapting a resume for a target role, checking whether the resume would pass ATS as-is, deciding what to add or remove for a role, matching experience and projects to job requirements, selecting evidence from resources, interviewing the candidate about past experience that might fit the job, or rendering a job-specific CV.'
argument-hint: 'Provide a job description file or prompt and the target role/company.'
---

# Resume Tailoring

## Purpose

Create a job-specific version of the resume in this repository from a job description — or judge whether the current resume passes the ATS screen for that role and list exactly what to change. The output is a concise, evidence-based RenderCV YAML resume, plus an ATS verdict and change list when requested. Nothing enters the resume that is not supported by the repository resources or confirmed by the candidate in the interview; do not invent experience, technologies, employers, metrics, or responsibilities.

## Repository Inputs

Use these files as the source of truth:

- `./resume.yaml` — the editable RenderCV resume YAML and primary output (the repository’s resume template).
- `./job_description.md` — the target job description when present.
- `./resources/experience.md` — detailed employment history and verified responsibilities.
- `./resources/projects.md` — completed projects and implementation details.
- `./resources/skills.md` — technologies and capabilities the candidate has used.
- `./resources/key_achievements.md` — verified high-level achievements.
- `./resources/enhancers.md` — soft skills and supporting strengths; do not create an `Enhancers:` resume section.
- `./.agents/skills/rendercv/SKILL.md` — RenderCV syntax and rendering guidance.
- `./.agents/AGENTS.md` — repository-specific constraints and goals.

If the user supplies a job description directly, use it instead of requiring `job_description.md`. Read the current YAML before editing because users or formatters may have changed it since the last run.

## Procedure

### 1. Inspect the current state

1. Read `./.agents/AGENTS.md` and the RenderCV skill instructions.
2. Read the current `./resume.yaml` in full or in meaningful sections.
3. Read the relevant resource files, including the detailed experience and project descriptions.
4. Identify the installed RenderCV version if it affects supported schema fields. Do not add fields documented for a newer version if the local renderer rejects them.
5. Note existing user edits and preserve them unless the user explicitly requests a change.

### 2. Analyze the target role

Extract and group the job description into:

- Core responsibilities
- Required technologies and platforms
- Data, software, cloud, and infrastructure practices
- Domain or regulatory context
- Leadership and collaboration expectations
- Preferred or bonus qualifications
- Important ATS keywords and equivalent terminology

Create an internal evidence map with three categories:

- **Direct evidence:** explicitly supported by the resume or resources; safe to state directly.
- **Adjacent evidence:** related experience that can be framed carefully without claiming the exact technology or practice.
- **Unsupported:** absent from the sources; do not add it merely because it appears in the job description.

For example, Airflow and Cloud Composer can support orchestration and workflow-platform experience, but they must not be rewritten as Kubernetes, Spark, Databricks, Delta Lake, or Unity Catalog experience unless the sources explicitly verify those technologies.

### 3. Deliver the ATS verdict

Score every extracted job-description requirement against the current resume text:

- **Matched:** present in the resume with exact or standard-synonym phrasing (for example, `orchestration: Airflow` on the resume matches "a modern orchestrator such as Dagster or Airflow" in the job description).
- **Rewordable:** supporting evidence is already on the resume, but not in terms an ATS would match; name the truthful job-description keyword to swap in.
- **Addable:** supported by `resources/` but absent from the resume; cite the supporting resource file for each one.
- **Gap:** unsupported anywhere; carries into the interview in step 4.

Also check the structural basics an ATS parse depends on: conventional headings, contact info at the top, selectable text, and no tables or graphics (see the standards step below).

Verdict:

- **Pass:** every required qualification is matched or rewordable, and at least half of the desirable qualifications are matched, rewordable, or addable. This is the bar behind a "95% chance" ask.
- **Fail:** otherwise.

Report the verdict with the coverage table. On a fail, produce the change list that reaches full coverage of required qualifications and maximum plausible coverage of desirable ones:

- **Add:** the addable items, each citing the resource file that supports it.
- **Reword:** the rewordable items with their target keyword.
- **Remove:** bullets that crowd out relevant content or dilute the target role.
- **Interview:** the gaps, carried into step 4.

If the user asked only for the verdict, stop after reporting it.

### 4. Interview for hidden experience

For each gap, ask the candidate whether they have done what the job description names, or a close equivalent. Grill them, one question at a time:

- Anchor each question in their actual history — name the job-description requirement plus the plausible hook from the resources ("the JD wants Snowflake cost optimization; at your last role you owned warehouse spend — did you tune query costs there?").
- Follow up on scale, metrics, and outcomes before accepting an answer.
- Record every confirmed fact with their exact wording, numbers, and scope; it joins the Add list with "confirmed in interview" as its evidence.
- A "no" closes the gap; that requirement stays out of the resume.

Completion: every gap has been asked and is either confirmed with evidence or closed.

### 5. Select and prioritize content

Prioritize content in this order:

1. Recent experience with direct relevance to the target role.
2. Quantified outcomes and measurable scale.
3. Reusable frameworks, platform services, automation, and developer-experience improvements.
4. Reliability, testing, observability, governance, security, and cost-efficiency evidence.
5. Domain experience relevant to the employer.
6. Collaboration, mentorship, communication, and leadership.
7. Older or less relevant details only when space permits.

Use the resources creatively, but do not combine separate facts in a way that creates a new unsupported claim. Preserve employers, locations, dates, and metrics from the source material.

### 6. Edit the resume YAML

Tailor the following sections as appropriate:

- `cv.headline` — align with the target role using supported experience and important keywords.
- `cv.sections.Summary` — write 3–4 concise, role-specific statements covering seniority, relevant platform capabilities, outcomes, and collaboration.
- `experience` — reorder or rewrite highlights to lead with the strongest evidence for the target role; remove low-value bullets when necessary.
- `Skills` — group verified technologies and capabilities into readable ATS-friendly lines. Do not list unsupported tools.
- `projects` — select only projects that reinforce the target role. Avoid duplicating every experience bullet.
- `Education` — use a proper RenderCV education list entry, for example:

  ```yaml
  Education:
    - institution: Example University
      area: Computer Science
      degree: Bachelor of Science
      location: City, ST
  ```

  Preserve the current education facts if the user has edited them. If the local RenderCV version renders the degree column too narrowly, use a compatible custom `education_entry` template or another version-supported layout; do not add unsupported schema fields.

Do not add an `Enhancers:` section. Blend relevant enhancer language into the summary, experience, or skills only when it is supported and useful.

### 7. Maintain ATS and readability standards

- Prefer conventional headings such as Summary, Experience, Skills, Projects, and Education.
- Keep all important content as selectable text in the generated PDF.
- Use exact job-description keywords when truthful, plus the candidate’s actual equivalent technologies.
- Avoid tables, graphics, columns, icons, or decorative structures that obscure text extraction unless the existing RenderCV theme handles them reliably.
- Keep the rendered resume to two pages or fewer when practical. Reduce redundancy before shrinking typography.
- Keep bullets action-oriented and specific, with scale or outcomes where verified.
- Quote YAML strings containing colons and escape or quote other YAML-sensitive punctuation when needed.

### 8. Validate and render

After editing:

1. Run workspace diagnostics on `resume.yaml`.
2. Render the source YAML with the locally installed RenderCV command.
3. Confirm PDF, HTML, Markdown, Typst, and PNG generation succeeds unless the user requested specific formats only.
4. Inspect the generated PNGs or PDF for page count, clipped text, bad wrapping, empty pages, malformed columns, and degree/date layout issues.
5. Confirm generated content matches the YAML and does not introduce unsupported claims.
6. If rendering fails, fix only relevant YAML or supported design/template settings and validate again. Do not edit generated output files manually.

## Completion Checklist

Before reporting completion, verify:

- The target job description was used.
- The ATS verdict was reported with a coverage table; on a fail, the change list was delivered.
- Every gap was asked in the interview before any editing proceeded.
- Every technology and metric in the tailored resume is supported by the repository sources or an interview confirmation.
- The most relevant requirements appear naturally in the headline, summary, skills, experience, or projects.
- Healthcare, regulated-data, or other domain experience is included when relevant and supported.
- Unsupported bonus technologies were not implied.
- Education uses valid RenderCV entry syntax.
- YAML diagnostics pass.
- RenderCV successfully generates the requested outputs.
- The PDF is readable, selectable, and preferably no more than two pages.
- The user is told which source file changed and whether rendering passed.

## Example Prompts

- “Tailor my resume for the Senior Data Platform Engineer role using `job_description.md`.”
- “Use this job description to create an ATS-friendly RenderCV resume, but do not claim experience with tools not in `resources`.”
- “Update the resume for a healthcare data engineering position and render the final PDF.”
- “Would my resume pass the ATS for `job_description.md` in its current state?”
- “What should I add or remove to maximize my ATS odds for this role?”
