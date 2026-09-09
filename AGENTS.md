# Agent instructions — ROI course authoring

## Skills

- **Slide courses:** Always read and follow `.agents/skills/course-generator/SKILL.md` and `.agents/skills/course-generator/examples/layout-templates.md` when creating, outlining, editing, or validating slides.
- **Labs:** Always read and follow `.agents/skills/lab-generator/SKILL.md` and `.agents/skills/lab-generator/examples/lab-template.md` when creating or editing files under `labs/`.

## Repository layout

- `course/` — slide Markdown and `images/`
- `labs/lab-NN-slug/` — each lab’s `README.md` plus `images/`
- Stock intro/outro slide images live in `course/images/`; copy/reuse those filenames; do not regenerate.

## Output expectations

- Prefer multi-file courses (`00-introduction.md`, `01-….md`, …) under `course/`; short single-deck courses may use one file.
- Same `<!-- course-title: … -->` in every chapter file.
- No ampersand (`&`) in slide or lab titles/body text (use “and”).
- Content chapters: Lab stub → What You Learned → Quizzes (default) → Questions and Answers.
- Questions and Answers: `Questions?` body **or** stacked + `images/qa.png`—pick one pattern per course.
- Labs use Overview → Objectives → Setup → Task N → Congratulations!; no Qwiklabs `ql-*` tags.
