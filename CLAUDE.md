# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Jekyll-based academic website using al-folio theme, deployed to GitHub Pages at https://willxxli.github.io. Owner: Zhuoran (Will) Li - PhD candidate in Finance at UQ Business School.

## Build & Development Commands

```bash
# Install dependencies
bundle install

# Local development server (http://localhost:4000)
bundle exec jekyll serve

# Production build
export JEKYLL_ENV=production && bundle exec jekyll build
```

**Ruby version**: 3.3 (configured in .github/workflows/deploy.yml)

## Key Configuration

### _config.yml
- `search_enabled: true` - Cmd+K search functionality
- `enable_darkmode: true` - Light/dark theme toggle
- `navbar_fixed: true`, `footer_fixed: true`
- `latest_posts: enabled: false` - Blog posts disabled on homepage

### Deployment
GitHub Actions workflow in `.github/workflows/deploy.yml`:
- Triggers on push to main/master
- Builds with Ruby 3.3 and deploys to gh-pages branch
- Uses `JamesIves/github-pages-deploy-action`

## Project Structure

```
_pages/           # Content pages (about.md, research.md, teaching.md, service.md, cv.md)
_layouts/         # Liquid templates (about.liquid, page.liquid, etc.)
_includes/        # Reusable components (header.liquid, footer.liquid, figure.liquid)
_sass/            # SCSS stylesheets (_base.scss, _themes.scss, _variables.scss)
_data/            # YAML data (cv.yml for structured CV data)
_bibliography/    # papers.bib for publications
assets/
  ├── img/        # Images (prof_pic_color.png, wechat-qr.jpg, cfa-certificate.jpg)
  ├── pdf/        # PDFs (cv-will-li.pdf)
  ├── js/         # JavaScript (theme.js, search/)
  └── json/       # resume.json
```

## Common Tasks

### Adding/Editing Pages
Pages in `_pages/` use frontmatter:
```yaml
---
layout: page
permalink: /pagename/
title: pagename
nav: true
nav_order: 2
---
```

### Adding Images
Use al-folio's figure include:
```liquid
{% include figure.liquid path="assets/img/image.jpg" title="Title" class="img-fluid rounded z-depth-1" %}
```

### CV Page
- `_pages/cv.md` uses `layout: none` and redirects to PDF via meta refresh
- CV PDF stored at `assets/pdf/cv-will-li.pdf`
- Structured CV data in `_data/cv.yml` (used by cv.liquid layout)

### Search Functionality
Ninja-keys component in `_includes/scripts/search.liquid`:
- Keyboard shortcut: Cmd+K / Ctrl+K
- Data populated from site pages and socials

## Architecture Decisions

| Feature | Implementation |
|---------|----------------|
| Theme | al-folio (academic portfolio) |
| Math | MathJax 3.2.2 (CDN) |
| Icons | FontAwesome + Tabler Icons |
| Image Zoom | medium-zoom |
| Comments | Giscus (currently disabled) |

## Removed/Disabled Features

From standard al-folio:
- jekyll-scholar plugin (removed for GitHub Pages compatibility)
- jekyll-archives plugin
- Publications page (simplified to Research interests only)
- News announcements
- Google Analytics

## Git Workflow

- Main branch: `main`
- Deployment branch: `gh-pages` (auto-generated)
- Remote: `git@github.com:willxxli/willxxli.github.io.git`
