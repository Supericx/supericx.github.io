# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Personal blog and portfolio site built with Jekyll, hosted on GitHub Pages.

## Development Commands

```bash
# Install dependencies
bundle install

# Serve locally with live reload and drafts (http://localhost:4000)
bundle exec jekyll serve --livereload --drafts

# Build only (output to _site/)
bundle exec jekyll build
```

## Site Architecture

### Content
- **Blog posts**: `_posts/YYYY-MM-DD-title.md` (requires `layout: post` and `title` in front matter)
- **Projects page**: `projects.md`
- **About page**: `me/index.md`
- **Homepage projects list**: `_data/websites.yml`
- **Archived posts**: `_posts/archive/` (excluded from build via `_config.yml`)

### Layouts
- `_layouts/default.html` - Base HTML template
- `_layouts/post.html` - Blog post template (extends default)
- `_layouts/about.html` - About page template (extends default)
- `_includes/header.html` - Site header with navigation

### Styling
- `assets/css/main.scss` - Main stylesheet, imports partials
- `_sass/_config.scss` - Variables: colors, fonts, typography scale, breakpoints
- `_sass/_reset.scss` - CSS reset
- Uses Inconsolata monospace font, modular scale typography (1.25 ratio)
- Single breakpoint at 600px for mobile

## Deployment

Automatic via GitHub Pages on push to master branch.
