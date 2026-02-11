# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Jekyll-based academic portfolio website built on the Academic Pages template, deployed via GitHub Pages. The site showcases publications, talks, CV, and research projects.

## Development Commands

### Local Development
```bash
bundle install  # Install Ruby dependencies (run once or after Gemfile changes)
jekyll serve -l -H localhost  # Start local server at localhost:4000 with live reload
bundle exec jekyll serve -l -H localhost  # Use specific bundle dependencies
```

Note: Configuration changes in `_config.yml` require stopping and restarting the Jekyll server.

### Docker Development
```bash
docker compose up  # Build and run site at localhost:4000
```

### JavaScript Build
```bash
npm run build:js  # Minify and bundle JavaScript
npm run watch:js  # Watch for JS changes and rebuild
```

## Site Architecture

### Content Collections
Jekyll collections organize content types. Each has a directory with markdown files:
- **`_publications/`**: Research papers, preprints, opinion pieces
- **`_talks/`**: Conference presentations, seminars, workshops
- **`_portfolio/`**: Project showcases (currently unused)
- **`_posts/`**: Blog posts (currently unused)
- **`_teaching/`**: Teaching materials (currently unused)
- **`_pages/`**: Static pages (about, cv, publications list, etc.)

### Collection Front Matter Structure

**Publications** (`_publications/*.md`):
```yaml
title: "Paper Title"
collection: publications
permalink: /publication/unique-slug
date: YYYY-MM-DD
venue: 'Journal Name or Conference'
category: 'manuscripts|preprints|opeds|books'  # Controls publication grouping
paperurl: 'https://doi.org/...'
citation: 'Full citation string'
```

**Talks** (`_talks/*.md`):
```yaml
title: "Talk Title"
collection: talks
type: "Conference presentation|Seminar|Workshop"
permalink: /talks/unique-slug
venue: "Event Name"
date: YYYY-MM-DD
location: "City, State/Country"
```

### Template System
- **`_layouts/`**: Page templates (single, talk, cv-layout, archive, etc.)
- **`_includes/`**: Reusable components (header, footer, sidebar, analytics, etc.)
  - `archive-single.html`: Template for listing items in collections
  - `author-profile.html`: Sidebar profile rendering
  - `cv-template.html`: CV generation from `_data/cv.json`
- **`_sass/`**: SCSS stylesheets compiled by Jekyll

### Configuration
- **`_config.yml`**: Main Jekyll config, site metadata, author info, collection settings
  - Update `author:` section to modify profile/bio/social links
  - `publication_category:` defines grouping headings for publications page
  - `collections:` defines content types and their URL structure
  - `defaults:` sets front matter defaults per collection
- **`_config_docker.yml`**: Docker-specific overrides
- **`_data/cv.json`**: Structured CV data (used by cv-layout template)
- **`_data/ui-text.yml`**: UI string translations

## Content Management Workflows

### Adding Publications Manually
1. Create new file in `_publications/` with format `YYYY-MM-DD-short-name.md`
2. Add front matter with required fields (title, date, venue, category, citation)
3. Add description/abstract in markdown body
4. Category determines grouping on publications page (see `_config.yml` publication_category)

### Adding Talks Manually
1. Create new file in `_talks/` with format `YYYY-MM-DD-event-name.md`
2. Add front matter with required fields (title, date, venue, location, type)
3. Add description in markdown body
4. Changes trigger GitHub Actions workflow to update talk map

### Batch Adding Content from TSV
Use Jupyter notebooks/Python scripts in `markdown_generator/` to generate multiple files:
- `publications.ipynb` / `publications.py`: Generate from `publications.tsv`
- `talks.ipynb` / `talks.py`: Generate from `talks.tsv`
- `PubsFromBib.ipynb` / `pubsFromBib.py`: Import from BibTeX
- `OrcidToBib.ipynb`: Fetch from ORCID

Run notebooks with: `jupyter notebook markdown_generator/`

### Updating CV
Edit `_data/cv.json` with structured data (education, work, skills, publications, etc.). The cv-layout template at `_layouts/cv-layout.html` renders it.

## GitHub Actions
**Talk Map Automation** (`.github/workflows/scrape_talks.yml`):
- Triggers on changes to `_talks/` directory or `talkmap.ipynb`
- Executes `talkmap.ipynb` to geocode talk locations
- Generates map visualization
- Auto-commits results

## Customization Points

### Styling
- Site theme: Set `site_theme` in `_config.yml` (options: default, air, sunrise, mint, dirt, contrast)
- Custom SCSS: Modify files in `_sass/`

### Profile/Author Info
- Update `author:` section in `_config.yml`
- Avatar: Place image in `images/` and set `author.avatar` filename

### Navigation
- Edit `_data/navigation.yml` to add/remove menu items (if file exists)
- Page visibility: Set `permalink` in page front matter

## Important Patterns

### Permalinks
- Collections use permanent URLs defined in `_config.yml` collections section
- Individual items override with `permalink:` in front matter
- Format: `/collection-name/item-slug/`

### Asset Management
- PDFs, slides: Upload to `files/` directory → accessible at `/files/filename.pdf`
- Images: Upload to `images/` directory
- Static JS/CSS: Placed in `assets/`

### Liquid Template Logic
- Archive pages iterate collections: `{% for post in site.publications %}`
- Use `{% include archive-single.html %}` to render collection items
- Category filtering: Check `post.category` or `post.type`

## Common Tasks

### Change Profile Picture
1. Add image to `images/` directory
2. Update `author.avatar` in `_config.yml`
3. Restart Jekyll server

### Add Social Media Link
1. Find relevant field in `author:` section of `_config.yml`
2. Add username or URL
3. Icon appears automatically in sidebar (if supported by theme)

### Modify Publication Groupings
1. Edit `publication_category:` in `_config.yml`
2. Ensure publication front matter `category` matches a defined category key

### Update Contact Email
1. Change `author.email` in `_config.yml`
2. Restart Jekyll server
