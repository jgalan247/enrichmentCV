# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A multi-page interactive educational site ("Word Skills Academy") for low-ability Year 9 students. The core purpose is teaching Microsoft Word skills through themed creative projects. No build system, no dependencies — just self-contained HTML files with inline CSS and JS, plus Google Fonts.

## Site Structure

| File | Purpose | Colour Theme |
|------|---------|--------------|
| `index.html` | Landing page — introduces the programme, links to all lessons, tracks progress via localStorage | Neutral/multi-colour |
| `cv.html` | **Compulsory** first lesson — Build Your CV | `--l1: #e63946` (red), `--l2: #2a9d8f` (green) |
| `newspaper.html` | Optional — School Newspaper (columns, WordArt, text wrapping) | `--l1: #1d3557` (blue), `--l2: #457b9d` |
| `travel.html` | Optional — Travel Guide (page borders, text boxes, itinerary tables) | `--l1: #2d6a4f` (green), `--l2: #d4a373` (sand) |
| `football.html` | Optional — Football Club Programme (headers/footers, numbered lists, league tables) | `--l1: #1b4332` (dark green), `--l2: #40916c` |
| `pet.html` | Optional — My Favourite Pet leaflet (spell check, find & replace, borders & shading) | `--l1: #7b2cbf` (purple), `--l2: #c77dff` |

Students must complete `cv.html` first, then at least 2 of the 4 optional lessons in any order. Progress is tracked in `index.html` via localStorage key `wordSkillsProgress`.

## Lesson Page Architecture

Each lesson file (~2900–3400 lines) follows the same pattern:

1. **`<style>`**: CSS custom properties (`:root` vars), responsive via media queries at bottom
2. **HTML body**: Panel-based navigation — sections are `<div id="panel-{name}">` toggled by JS. Standard panels: `compare`, `l1-intro`, `l1-skill`, `l1-ws`, `l2-intro`, `l2-skill`, `l2-ws`
3. **`<script>`**: Vanilla JS with shared function patterns:
   - `showPanel(id, btn)` / `goTo(id)` / `updateNavDone()` — tab navigation with completion tracking
   - `CAT_FEATURES` array + `catBuild/catPlace/catCheck` — drag-and-drop categorisation
   - `matchClick()` — card matching game state machine
   - `initSort/checkSort/shuffleSort` — drag-to-reorder activities
   - `answerQ(el, correct)` — quiz with retry-on-wrong
   - `toggleCheck(el)` — checklists
   - Live preview builders — form inputs rendering into styled preview panes

## Development

No build tools — open any HTML file directly in a browser. To serve locally:

```
python3 -m http.server 8000
```

## Key Conventions

- Each page is fully self-contained (inline CSS + JS) — do not split into separate files unless explicitly asked
- Colour theming uses CSS custom properties per lesson; Lesson 1 content uses `--l1`, Lesson 2 uses `--l2`
- All interactivity is vanilla DOM manipulation — no libraries or frameworks
- Mobile support via touch-tap alternatives for all drag-and-drop activities
- Panel IDs follow `panel-{name}` with nav tabs using `data-panel` attributes
- Target audience is low-ability UK Year 9 students (age 13–14) — language should be simple, instructions highly scaffolded, activities engaging and varied
