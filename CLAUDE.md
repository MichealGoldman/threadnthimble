# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

threadnthimble is a static website for "Thread & Thimble" — plain HTML/CSS with no build step, no package manager, and no JavaScript framework. There is no `package.json`, bundler, linter, or test suite in this repo.

## Development

There are no build/lint/test commands — edit the HTML/CSS files directly and preview by opening them in a browser (e.g. `start index.html` or via a local static server such as `npx serve`).

## Architecture

- `index.html` — landing page, uses the `.hero` / `.hero-card` layout to introduce the site and link to `videos.html`.
- `videos.html` — hub page listing links to the individual topic pages (`practical-hand-sewing.html`, `visible-mending.html`, `cross-stitch.html`, `embroidery.html`, `sashiko.html`) via `.button-row`.
- `practical-hand-sewing.html`, `visible-mending.html`, `cross-stitch.html`, `embroidery.html`, `sashiko.html` — one page per topic, each using the `.site-header` + `.page` + `.video-grid` layout. Each embeds YouTube videos via `<iframe src="https://www.youtube.com/embed/...">` inside `.video-card` / `.video-wrapper` elements. These pages currently share the same placeholder embedded video IDs — when adding real content, follow the existing page's structure and swap in the topic-specific YouTube embed IDs/titles.
- `styles.css` — single shared stylesheet for all pages. Theming is done via CSS custom properties defined on `:root` (`--background`, `--surface`, `--text`, `--muted`, `--accent`, `--accent-dark`, `--border`, `--shadow`). Reuse these variables rather than hardcoding new colors. Responsive breakpoints are at `900px` (video grid collapses to one column) and `600px` (spacing adjustments).

## Conventions

- New pages should include the shared `<link rel="stylesheet" href="styles.css">` and reuse existing classes (`.hero`, `.hero-card`, `.page`, `.page-heading`, `.site-header`, `.video-grid`, `.video-card`, `.button`, `.nav-link`) instead of introducing new one-off styles.
- Video pages link back to `index.html` via the `.brand` logo and a `.nav-link` "Home" link in `.site-header`.
