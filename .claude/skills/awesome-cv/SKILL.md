---
name: awesome-cv
description: Generate a new resume, CV, or cover letter as LaTeX using the Awesome-CV template that lives in this repo (awesome-cv.cls + examples/). Use whenever the user asks to create, draft, tailor, or update a resume/CV/cover letter here, or says things like "make me a new resume", "tailor my CV for X job", "write a cover letter for this posting", or drops job details and asks for an application. Also use when the user provides raw personal history (jobs, education, skills) and wants it turned into a polished PDF-ready CV using this template.
---

# Awesome-CV: New Resume / CV / Cover Letter

This repo IS the Awesome-CV LaTeX template (`awesome-cv.cls` at the root, working samples under `examples/`). The job of this skill is to produce a new, coherent LaTeX document that compiles against this class, without inventing commands the class doesn't ship.

## Anchors: read before writing

- `awesome-cv.cls` — the source of truth for every command you can use. When unsure whether something like `\cventry`, `\cvskill`, or `\photo` accepts a given argument, grep this file first. Do not guess macros.
- `examples/resume.tex` — one-page style, section-includes via `\input{resume/*.tex}`.
- `examples/cv.tex` — longer form, includes a `skills.tex` section.
- `examples/coverletter.tex` — cover letter shell (`\recipient`, `\lettersection`, `cvletter` environment).
- `examples/resume/*.tex`, `examples/cv/*.tex` — canonical shape for each section.

If the user's request maps to something already demonstrated in `examples/`, mirror that file's structure rather than inventing a new layout.

## What to ask before drafting

Ask only what you actually need. Skip questions the user already answered.

1. **Kind of document**: résumé (one-page), CV (long form), or cover letter — or a combined set.
2. **Whose CV**: name, contact info, one-line position, socials to display. If the user is the owner of the repo and hasn't said otherwise, offer to reuse the header from an existing `.tex` in `examples/` (or from a prior CV they point to).
3. **Content**: work experience, education, skills, honors, certificates, projects. Accept it in any format — a paste, a link, an existing PDF, a rough list — and normalize it.
4. **Target role or job posting** (if tailoring): copy or link. Use it to reorder bullets, pick which sections appear, and tune wording — never to fabricate experience.
5. **Style choices** (optional, sensible defaults if silent): accent color (`awesome-red` default; other options listed in `resume.tex`), paper size (`a4paper` default), whether to include a photo.

## Output layout

Write new documents in a fresh directory so nothing under `examples/` gets clobbered. Default layout:

```
<name>-resume/
├── resume.tex            # main file, \documentclass{awesome-cv}
└── resume/
    ├── summary.tex
    ├── experience.tex
    ├── education.tex
    ├── skills.tex        # optional
    ├── honors.tex        # optional
    └── certificates.tex  # optional
```

The main `.tex` must be placed so that `\documentclass{awesome-cv}` can find `awesome-cv.cls`. Two workable options:

- Put the new folder at the repo root as a sibling of `awesome-cv.cls` (simplest, matches how `examples/` works).
- Or `\usepackage{awesome-cv}` after adjusting `TEXINPUTS`. Prefer the first unless the user asks otherwise.

## Section templates

All sections wrap a `\cvsection{...}` header around one of these environments. Copy the shape from the matching `examples/` file — don't paraphrase it.

**Work experience** — `cventries` of `\cventry{title}{org}{location}{dates}{ items }`, where the item block is either empty `{}` or a `cvitems` environment of `\item {...}` lines.

**Education** — same `\cventry` shape; degree in the title slot, institution in the org slot.

**Skills** — `cvskills` of `\cvskill{category}{comma-separated list}`.

**Honors / certificates** — `cvhonors` of `\cvhonor{award}{event}{location}{date}` (for certs: name / issuer / credential ID / date).

**Summary** — `cvparagraph` with free prose. Keep it 2–4 sentences, first-person or implied-subject; match tone of the target role.

**Cover letter** — `cvletter` with `\lettersection{...}` blocks; header comes from `\recipient`, `\letterdate`, `\lettertitle`, `\letteropening`, `\letterclosing`, `\letterenclosure`.

See `references/commands.md` for the full macro cheat sheet with argument order, and the special characters that must be escaped (`%`, `&`, `#`, `$`, `_`, `{`, `}`, `~`, `^`, `\`).

## Writing style for bullets

The template rewards concise, verb-led bullets. Read `references/bullets.md` before writing experience bullets — it captures the pattern the existing `examples/resume/experience.tex` uses (impact + how, past tense, single sentence, LaTeX-safe punctuation).

## Compiling to PDF

Awesome-CV requires XeLaTeX. The repo's `Makefile` at the root already does the right thing for the samples; for a new document:

```
xelatex -interaction=nonstopmode -halt-on-error <main>.tex
xelatex -interaction=nonstopmode -halt-on-error <main>.tex   # second pass for refs
```

If TeX Live isn't installed in this environment, don't try to install it — hand the user the `.tex` files and tell them how to build (Overleaf, local XeLaTeX, or the Docker path documented in the README).

## Tailoring an existing CV to a job

When the user provides a job posting and asks to tailor:

1. Read their existing `.tex` (theirs, not the `examples/` samples) — treat it as ground truth for facts.
2. Extract the posting's must-haves and nice-to-haves.
3. Rewrite the summary to speak to the role.
4. Reorder experience bullets so the most role-relevant ones lead each `\cventry`. Drop clearly off-topic bullets; do not invent new ones.
5. Reorder or add categories in `skills.tex` to surface matching stack.
6. Optionally add a short cover letter using the `coverletter.tex` shape.

Never fabricate employers, dates, titles, or metrics. If a claim in the posting has no basis in the source CV, leave it out and mention the gap to the user.

## What to hand back

- The `.tex` files, written into the new folder.
- A one-line note on how to compile (or a `make` target if adding one is trivial).
- If a PDF was produced, its path.
- A short list of any facts you left out because the source didn't support them.
