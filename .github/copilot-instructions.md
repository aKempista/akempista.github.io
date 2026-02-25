# Copilot Instructions for akempista.github.io

## Project Overview

This is a **Jekyll-based portfolio website** showcasing Aiden Kempista's physical and digital fabrication projects. The site emphasizes visual presentation with carousel images, project filtering by category, and highlighted featured projects.

## Architecture & Key Components

### Content Structure
- **`_projects/`**: Project markdown files with frontmatter (title, description, images, category, highlight flag)
- **`_layouts/`**: Templates inherited via Jekyll's layout system
  - `default.html`: Main site template with header/footer (282 lines, complex CSS-in-HTML)
  - `project.html`: Individual project detail page wrapper
- **`index.html`**: Homepage with filtered project grid and carousel controls
- **`_config.yml`**: Jekyll configuration with `collections: projects` for site.projects access

### Data Flow
Projects flow: `_projects/*.md` (YAML frontmatter) → Jekyll collection → `site.projects` (Liquid template access) → rendered HTML in `_site/`

### Design System
CSS is embedded in `default.html` with CSS custom properties (variables):
- `--primary`: #1c1c1c (dark background)
- `--secondary`: #CFB53B (gold accents)
- `--highlight`: #4281A4 (blue headers)
- `--text`: #FFFFF5 (off-white text)

## Critical Patterns & Conventions

### Project Frontmatter Format
```yaml
---
title: "Project Name"
category: "Category Name"  # Single category string, case-sensitive
description: "Brief description"
images:
  - /images/image1.jpg
  - /images/image2.jpg
highlight: false  # Boolean; true projects display in hero section + badge
layout: project
---
```

### Filtering & Display Logic
- **Homepage**: Uses Liquid `where` filters to find highlighted project and dynamically build category buttons from all project categories
- **Category filtering**: JavaScript-based (data-category attributes), case-normalized to lowercase
- **Image carousels**: JavaScript buttons (`.prev`, `.next`) cycle images; first image has `class="active"`

### Important Implementation Details
1. **Lazy loading**: Project grid images use `loading="lazy"`
2. **URL generation**: `relative_url` filter used for all paths (important for GitHub Pages subdirectory deployment)
3. **Dynamic buttons**: Category buttons generated from unique project categories, not hardcoded
4. **Back link**: Project detail pages include back link using `{{ "/" | relative_url }}`

## Developer Workflows

### Building & Previewing
```bash
bundle install           # Install Jekyll dependencies
bundle exec jekyll serve # Local preview at http://localhost:4000
```

### Adding a New Project
1. Create `_projects/projectname.md` with proper frontmatter (see template above)
2. Add image files to `/images/`
3. Set `highlight: true` if it should appear in hero section
4. Test filtering in browser (categories auto-generate)

### Modifying Styles
- Edit CSS variables in `default.html` `<style>` block (lines ~15-19)
- All colors reference CSS custom properties
- Note: `project.html` includes inline styles (margin, padding, background-color) that override defaults

## External Dependencies & Integration

- **Jekyll**: Static site generator (v4+ likely, defined in Gemfile if present)
- **Google Fonts**: Montserrat (700 weight), Lora (700 weight), Asimovian fonts loaded via CDN
- **GitHub Pages**: Site deploys to `akempista.github.io` (standard GitHub Pages setup)
- **Favicon**: `favicon-32x32.png` required in root directory

## Common Gotchas

- **Category field**: Projects use singular "category" (not "categories"), though index.html parses it as an array-like structure via `| join: ','`
- **Image paths**: Must start with `/images/` for proper resolution on GitHub Pages
- **Liquid filters**: `| downcase | strip` used for category normalization in filtering
- **Layout inheritance**: All project files reference `layout: project`, which wraps content in `default.html`

## When Making Changes

For style updates, carousel fixes, or category logic: review [index.html](index.html) for Liquid template patterns and [_layouts/default.html](_layouts/default.html) for styling. When adding projects, match the exact frontmatter structure in [_projects/accelero.md](_projects/accelero.md).
