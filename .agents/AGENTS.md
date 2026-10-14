This repository contains a templated resume. The goal is to use an AI agent to accept a job description (`./job_description.md`) and, using `./resources`, produce a job-description-specific version of the resume (`./<Name>_CV.yaml`; see `./Sample_CV.yaml` for a filled example) that renders correctly with RenderCV.

Here are the components of `./resources` and what they mean:

**enhancers**: Generic soft skills and traits that can be blended into the resume. This is NOT its own section — do not add an `Enhancers:` key to the YAML.
**skills**: Technologies and capabilities the candidate can include in a resume.
**experience**: Current and past employers and experience. Preserve employers, locations, and dates from this source.
**key_achievements**: High-level skills and achievements.
**projects**: Actual work completed. Use as a `Projects:` section or blend into job experience.
**file_pipeline**: Example deep-dive for a flagship project. Use for project-description prompts and role-tailored project sections; the short bullet version lives in `projects.md`.
**education**: Verified education facts. Always include an `Education:` section from this source.

When possible, aim to keep the rendered resume to two pages or less.

Resumes are generated using RenderCV with this skill: `.agents/skills/rendercv/SKILL.md`

New resumes are built from scratch, with the `resources/` files filled by interview, using `.agents/skills/new-resume/SKILL.md`

Resumes are tailored to a provided job description using `.agents/skills/resume-tailoring/SKILL.md`
