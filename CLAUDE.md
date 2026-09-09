# ROI course authoring

This repository is for authoring ROI Training slide courses and labs.

## Mandatory skills

Before creating or editing **slide decks**, read and follow:

- `.agents/skills/course-generator/SKILL.md`
- `.agents/skills/course-generator/examples/layout-templates.md`

Before creating or editing **labs**, read and follow:

- `.agents/skills/lab-generator/SKILL.md`
- `.agents/skills/lab-generator/examples/lab-template.md`

## Layout

- Slides: `course/` (Markdown chapters + `course/images/`)
- Labs: `labs/lab-NN-slug/README.md` + `images/`
- Reuse stock slide images in `course/images/` (`welcome.png`, `agenda.png`, `who-should-attend.png`, `prerequisites.png`, `qa.png`, ROI logo). Do not regenerate them.
- Default chapter quizzes after What You Learned (see Course Generator skill).

## Preview

Slides: https://roitraining.github.io/md-to-html-slides-viewer/  
Labs: https://github.com/roitraining/md-to-html-lab-viewer  
