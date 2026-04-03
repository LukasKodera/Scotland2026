# Scotland 2026 Trip Planner — CLAUDE.md

## Project Overview

A single self-contained HTML file for planning and presenting a trip to Scotland in 2026.
No frameworks, no build tools — everything lives in one `index.html` file.

## Output

- **File:** `index.html`
- **Format:** Single HTML file with embedded CSS and JS (no external dependencies)
- **Purpose:** Local browser presentation, not a deployed website

## Rules

- Keep everything in one `index.html` file — no separate CSS/JS files
- No external CDN dependencies; if styling is needed, write it inline
- The page must work fully offline (no fetch calls, no external resources)
- Do not add frameworks (React, Vue, etc.)

## Token Optimization Rules

- Use `haiku` model for mechanical subagent tasks (HTML/CSS edits, simple spec checks)
- Use `sonnet` only for content-heavy tasks (all 10 day cards) or final code reviews
- Skip code quality review for pure HTML/CSS tasks with no logic
- When reading large files, use `offset` + `limit` — never read the full file if only one section is needed
- Spec reviewers should grep for specific strings rather than reading the whole file when possible
- Skip the visual companion server for future iterations — use terminal descriptions instead

## GitHub Rules

- **Never merge to `main` directly** — always create a Pull Request
- GitHub token is stored in `ClaudeToken.txt` (never commit this file)
- All changes go through PRs, no exceptions

## Content Tracking

### Sections planned
- [x] Trip overview (dates, travelers, summary)
- [x] Day-by-day itinerary
- [x] Map / route overview
- [x] Accommodation list
- [x] Key links and resources

### Decisions log
- 2026-04-02: Chose single HTML file format for local presentation
- 2026-04-02: Built index.html — Nature & Fresh theme, timeline layout, rich day cards, light JS
