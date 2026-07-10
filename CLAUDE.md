# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

threadnthimble is a static website for "Thread & Thimble" — plain HTML/CSS with no build step, no package manager, and no JavaScript framework. There is no `package.json`, bundler, linter, or test suite in this repo.

## Development

There are no build/lint/test commands — edit the HTML/CSS files directly and preview by opening them in a browser (e.g. `start index.html` or via a local static server such as `npx serve`).

## Architecture

- `index.html` — landing page at the repo root, uses the `.hero` / `.hero-card` layout to introduce the site and link to `videos.html`.
- `videos.html` — hub page at the repo root listing links to the individual topic pages under `videos/` as a `.link-list` (vertical list of `.button`-styled links).
- `videos/` — one page per topic (`practical-hand-sewing.html`, `visible-mending.html`, `cross-stitch.html`, `embroidery.html`, `sashiko.html`), each using the `.site-header` + `.page` + `.video-grid` layout. Each embeds YouTube videos via `<iframe src="https://www.youtube.com/embed/...">` inside `.video-card` / `.video-wrapper` elements. These pages currently share the same placeholder embedded video IDs — when adding real content, follow the existing page's structure and swap in the topic-specific YouTube embed IDs/titles.
- `css/styles.css` — single shared stylesheet for all pages. Theming is done via CSS custom properties defined on `:root` (`--background`, `--surface`, `--text`, `--muted`, `--accent`, `--accent-dark`, `--border`, `--shadow`). Reuse these variables rather than hardcoding new colors. Responsive breakpoints are at `900px` (video grid collapses to one column) and `600px` (spacing adjustments).

## Conventions

- Pages at the repo root (`index.html`, `videos.html`) reference the stylesheet as `css/styles.css`; pages inside `videos/` reference it as `../css/styles.css` and link home as `../index.html`. Keep these relative paths in sync with a page's location if it moves.
- New pages should include the shared stylesheet link and reuse existing classes (`.hero`, `.hero-card`, `.page`, `.page-heading`, `.site-header`, `.video-grid`, `.video-card`, `.button`, `.nav-link`) instead of introducing new one-off styles.
- Video pages link back to the home page via the `.brand` logo and a `.nav-link` "Home" link in `.site-header`.
