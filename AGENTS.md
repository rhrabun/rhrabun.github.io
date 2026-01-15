# AGENTS.md

This repository contains a Jekyll-based personal website hosted on GitHub Pages. It's a minimalist portfolio site showcasing professional experience and projects.

## Project Structure

```
.
├── index.html          # Main page with Liquid templates
├── style.css           # Styles with dark mode support
├── _config.yml         # Jekyll configuration
├── _data/
│   ├── jobs.yml        # Professional experience data
│   └── projects.yml    # Projects data
└── assets/             # Static assets (images, SVGs)
```

## Build & Development Commands

### Local Development
```bash
# Install Bundler (if not already installed)
gem install bundler

# Install Jekyll and dependencies
bundle install

# Serve locally at http://localhost:4000
bundle exec jekyll serve

# Serve with drafts included
bundle exec jekyll serve --drafts

# Build the site for production
bundle exec jekyll build
```

### Deployment
Push changes to `main` branch. GitHub Pages automatically deploys.

## Code Style Guidelines

### CSS
- **Naming**: BEM (Block Element Modifier) convention
  - Blocks: `.intro`, `.timeline`, `.bio`
  - Elements: `.intro__photo`, `.timeline__item`, `.timeline__dot`
  - Modifiers: `invert` (for dark mode)
- **Theming**: Use CSS custom properties for theme support
  - Define in `:root`: `--bg`, `--text`, `--link`, `--code-bg`, `--shadow`
  - Dark mode overrides in `[data-theme="dark"]`
- **Responsive**: Use mobile-first approach with `@media (max-width: 600px)`
- **Formatting**: 4-space indentation, properties on separate lines

### HTML & Liquid Templates
- **Front Matter**: Start with `---` on first line (can be empty)
- **Liquid Syntax**: `{% for item in site.data.collection %}` for iteration
- **Filters**: Use `| markdownify` for markdown content in YAML data
- **Attributes**: Use lowercase, quote attribute values
- **Accessibility**: Include `alt` attributes on images, `aria-label` on buttons

### YAML Data Files
- **Multi-line strings**: Use `>` for folded scalars (preserves newlines as spaces)
- **Lists**: Use hyphen prefix `-` for array items
- **Markdown**: Content should support markdown, filtered with `| markdownify` in templates
- **Structure**: Keys should be lowercase with underscores (e.g., `company`, `position`)

### JavaScript
- **Style**: Vanilla JavaScript, no frameworks
- **Variables**: Use `const` for constants, `let` for reassignable variables
- **Event Handling**: Use `addEventListener` over inline event handlers
- **Storage**: Use `localStorage` for user preferences (theme, etc.)
- **Formatting**: 4-space indentation, semicolons optional but recommended

### Naming Conventions
- **Files**: lowercase with hyphens (`my-file.html`, `my-style.css`)
- **CSS Classes**: BEM naming (`.block__element--modifier`)
- **JavaScript**: camelCase for variables/functions (`getElementById`, `addEventListener`)
- **YAML Keys**: lowercase with underscores (`company_name`, `job_description`)

### Formatting
- **Indentation**: 4 spaces (no tabs)
- **Line Length**: Aim for ~100 characters, break as needed
- **Blank Lines**: Single blank line between logical sections
- **Trailing Spaces**: Remove all trailing whitespace

### Dark Mode Implementation
- Use `data-theme="dark"` attribute on `<html>` element
- Save preference in `localStorage.getItem("theme")`
- Toggle with button using `.invert` class on icons
- CSS filter `invert(1)` for dark mode icon handling

## Content Guidelines

### Adding Job Experience
Add entries to `_data/jobs.yml`:
```yaml
- company: Company Name
  position: Job Title
  dates: Month Year – Present
  description: >
    Brief description of role and responsibilities.
    Supports markdown syntax.
```

### Adding Projects
Add entries to `_data/projects.yml`:
```yaml
- title: Project Title
  role: Your Role
  description: >
    Project description.
    Supports markdown lists:
      * First item
      * Second item
```

### Adding Assets
Place images in `assets/` directory. Use relative paths:
- Images: `assets/image-name.webp` (prefer WebP format)
- Icons: SVG format, use `.invert` class for dark mode

## Testing & Validation

### HTML Validation
```bash
# Install html5validator (if needed)
gem install html5validator

# Validate HTML
html5validator --directory _site
```

### Linting
No linter configured currently. Consider adding:
- CSS: `stylelint` for CSS linting
- HTML: `htmlhint` or `htmllint`
- YAML: `yamllint` for YAML validation

## Git Workflow

- **Main branch**: `main` (production)
- **Commit messages**: Conventional Commits format (optional but recommended)
- **No tags**: Version tracking not needed
- **Pull requests**: Not strictly required but recommended for larger changes

## Browser Support

- Modern browsers (Chrome, Firefox, Safari, Edge)
- Mobile-responsive (600px breakpoint)
- Dark mode supported via CSS custom properties
- Minimal dependencies for fast loading

## Performance Notes

- Use WebP format for images when possible
- Minimize asset sizes
- Leverage browser caching (GitHub Pages handles this)
- CSS is already minimized inline in `<head>`

## Common Patterns

### Theme Toggle
Use existing pattern in `index.html` for any theme-related features:
```javascript
const html = document.documentElement;
const savedTheme = localStorage.getItem("theme");
// Toggle logic
html.setAttribute("data-theme", "dark");
```

### Timeline Layout
Reuse `.timeline` class for any chronological content:
```html
<div class="timeline">
  <div class="timeline__item">
    <div class="timeline__dot"></div>
    <div class="timeline__content">
      <!-- Content -->
    </div>
  </div>
</div>
```

## Notes

- No tests are currently configured
- No CI/CD pipeline (GitHub Pages handles deployment)
- Keep changes minimal and focused
- Prioritize simplicity over complexity
- All content is static - no server-side logic
