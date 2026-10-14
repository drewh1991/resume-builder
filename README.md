# Resume Builder

A repository to organize, version control, and generate a resume. Your history
lives as plain Markdown evidence files under `resources/`; a RenderCV YAML file
turns that evidence into a publication-quality PDF (plus HTML, Markdown, Typst,
and PNG). AI agent skills drive the workflow — one interviews you to build the
file set, one tailors it to a job description.

## How it works

- `from_existing.md` — optionally paste an existing resume here as a starting point.
- `resources/` — the source of truth: education, experience, projects, skills,
  achievements, and enhancers. Every claim on the resume must trace back to one
  of these files.
- `<Name>_CV.yaml` — the RenderCV resume. It renders to PDF/HTML/Markdown/Typst/PNG
  via Typst.
- `job_description.md` — paste a target job description here before tailoring.
- `.agents/skills/` — the agent skills that operate on the above.

## Install

Requires [uv](https://docs.astral.sh/uv/), which installs the pinned Python and
RenderCV for you.

```bash
git clone <repository-url> resume
cd resume
uv sync
uv run rendercv --version   # confirm RenderCV is available
```

## Get started: bootstrap your resume

1. (Optional) Paste your existing resume into `from_existing.md`, or leave it
   empty to start from scratch.
2. Invoke the `new-resume` skill. The agent will:
   - read `from_existing.md` and any existing `resources/` files,
   - interview you in rounds until every resource file is complete,
   - write each file under `resources/`,
   - scaffold and render `<Name>_CV.yaml`.
3. To experiment with rendering on your own, try the bundled template:

   ```bash
   uv run rendercv render Sample_CV.yaml
   ```

## Tailor to a job description

1. Create a git branch for the application so each tailored resume is isolated
   and reviewable:

   ```bash
   git checkout -b apply/<company>-<role>
   ```

2. Paste the target job description into `job_description.md`.
3. Invoke the `resume-tailoring` skill. The agent will:
   - extract the job's requirements and score them against your current resume,
   - report an ATS verdict (Pass/Fail) with a coverage table,
   - add, reword, or remove content using only evidence from `resources/`,
   - render the tailored resume and confirm the outputs.
4. Find the generated output in `rendercv_output/`.

## Skills

- `new-resume` — interview-driven bootstrap of the resume and `resources/` files.
- `resume-tailoring` — tailor the resume to a job description and judge ATS fit.
- `rendercv` — RenderCV YAML schema and rendering reference.
