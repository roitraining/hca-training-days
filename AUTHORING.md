# Authoring guide (instructors)

How to create an ROI Training course with this template and an AI coding agent.

## 1. Create your repository

- Prefer **GitHub → Use this template** so you get a clean course repo.
- Or copy this folder and `git init`.

You do **not** need the slides viewer or lab viewer source code in your repo.

## 2. Open in your editor

Use any editor with a coding agent:

- Cursor  
- Visual Studio Code + GitHub Copilot  
- Claude Code  
- Antigravity / Gemini  

Pointer files in this repo (`.cursorrules`, `CLAUDE.md`, `AGENTS.md`, `.github/copilot-instructions.md`) tell the agent to follow the Course Generator and Lab Generator skills. You should not need global machine setup.

If the agent seems unaware of the rules, say explicitly:

> Read `.agents/skills/course-generator/SKILL.md` and `.agents/skills/lab-generator/SKILL.md`, then follow them.

## 3. Course layout (slides)

```text
course/
  00-introduction.md
  01-your-first-chapter.md
  02-…
  images/
    roi-logo-with-name.png   # stock — do not regenerate
    welcome.png
    agenda.png
    who-should-attend.png
    prerequisites.png
    qa.png
    …                        # your diagrams / screenshots
```

- **Multi-chapter courses:** one Markdown file per chapter (required by the skill).
- **Stock images** are already in `course/images/`. Copy them into place for every new course folder if you split courses later; do not reinvent them.
- Replace `course/sample-course.md` with your real chapters when you start (or keep it as a layout reference).

## 4. Labs layout

```text
labs/
  lab-01-getting-started/
    README.md
    images/
  lab-02-…
```

Follow:

- [.agents/skills/lab-generator/SKILL.md](.agents/skills/lab-generator/SKILL.md)
- [.agents/skills/lab-generator/examples/lab-template.md](.agents/skills/lab-generator/examples/lab-template.md)

See also [labs/README.md](labs/README.md) and the sample at `labs/lab-01-sample-lab-viewer-format/`.

### Lab stubs on slides

Chapter endings include a **lab stub** (title, time, link only). Point the link at the lab folder, for example:

`labs/lab-01-getting-started/`

Do not write full lab steps in the slide deck.

## 5. Work with the agent

Suggested sequence:

1. Share audience, duration, and objectives.
2. Ask for an **outline** (chapters → sections → labs) and confirm it.
3. Ask the agent to **write** `course/00-introduction.md` and each chapter file.
4. Ask the agent to **write** each lab under `labs/lab-NN-slug/` using the Lab Generator skill.
5. Ask it to run each skill’s **validation checklist**.
6. You review slides and labs in their viewers; fix content and visuals as needed.

## 6. Preview

### Slides

1. Push your repo to GitHub (public, or ensure the viewer can read it).
2. Open the [HTML Slides Viewer](https://roitraining.github.io/md-to-html-slides-viewer/).
3. **Open → GitHub**, paste the URL to your `course/` folder (or a single `.md` file).

Local alternative: run any static server in a checkout of the slides viewer and pass `?course=` at your Markdown URL.

### Labs

Use the [md-to-html-lab-viewer](https://github.com/roitraining/md-to-html-lab-viewer) once lab files exist.

## 7. What not to do

- Do not paste an entire multi-chapter course into one mega-file (unless you intentionally author a short single-file workshop and accept that it diverges from the default skill).
- Do not invent instructor bios on the Welcome slide.
- Do not use `&` in slide titles/body (write “and”; use **Questions and Answers**, not “Q&A”).
- Do not regenerate the stock intro/outro images—reuse the files in `course/images/`.
- Do not put full lab procedures in slide Markdown—use `labs/` and the Lab Generator skill.
- Do not use Qwiklabs `ql-*` tags or fragments in Lab Viewer manuals.

## 8. Skill reference

- Course: [.agents/skills/course-generator/SKILL.md](.agents/skills/course-generator/SKILL.md)  
- Course templates: [.agents/skills/course-generator/examples/layout-templates.md](.agents/skills/course-generator/examples/layout-templates.md)  
- Labs: [.agents/skills/lab-generator/SKILL.md](.agents/skills/lab-generator/SKILL.md)  
- Lab template: [.agents/skills/lab-generator/examples/lab-template.md](.agents/skills/lab-generator/examples/lab-template.md)  
