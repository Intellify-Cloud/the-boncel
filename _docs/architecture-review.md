# Code Architecture Review: The Bond Cellar

## Executive Summary

The Bond Cellar is a Jekyll-based static website for a bond origination business in South Africa. The codebase demonstrates a well-structured approach to static site generation but has several areas for improvement around maintainability, security, and modern best practices.

---

## Architecture Overview

### Stack Summary

| Component | Technology | Version |
|-----------|------------|---------|
| Static Site Generator | Jekyll | ~> 4.0 |
| CSS Framework | Bootstrap | 4.3.1 |
| JavaScript | jQuery + Bootstrap JS | 3.4.1 / 4.3.1 |
| Build Tool | Webpack 4 | 4.40.2 |
| Icons | FontAwesome | 5.9.0 |
| Font | Roboto (Google Fonts) | - |

### Project Structure

```
├── _assets/           # Source assets (SCSS, JS)
│   ├── base/          # Base styles (variables, mixins, page)
│   ├── components/    # Component styles (buttons, navbar)
│   └── layout/        # Layout styles (services, team, clients, etc.)
├── _config.yml        # Jekyll configuration
├── _includes/         # Reusable HTML partials
├── _layouts/          # Page layouts (default, home, page)
├── _data/             # YAML data files for content
├── _site/             # Generated static site (output)
└── assets/            # Bundled JS/CSS (compiled output)
```

---

## Code Standards & Best Practices Review

### ✅ Strengths

#### 1. Modular SCSS Architecture
- Well-organized into `base/`, `components/`, and `layout/` directories
- Use of CSS custom properties for design tokens
- Bootstrap variable overrides before import (proper order)

#### 2. Separation of Concerns
- Content in markdown files
- Presentation in includes
- Configuration in `_config.yml` and `_data/*.yml`
- Styles modularized by component

#### 3. Accessibility Features
- `aria-label` on hero section
- `aria-hidden` on decorative icons
- Proper semantic HTML structure
- Focus management in button styles

#### 4. Performance Considerations
- Image lazy loading on client logos
- Font preconnect headers
- Asset bundling via Webpack
- CSS minification in production

### ⚠️ Issues & Recommendations

#### 1. Security Issues

**Inline JavaScript in page.html (lines 6-10)**
```html
<script>
document.getElementById("page-top").className="bg-light";
</script>
```
- **Issue**: Using JavaScript to change CSS classes when CSS could handle this
- **Fix**: Use Liquid conditionals to add a class to the body element, or use CSS attribute selectors

**Hardcoded Analytics ID (G-XXX)**
- **Issue**: Placeholder analytics ID in production code
- **Fix**: Use environment variables or separate config for sensitive values

#### 2. JavaScript Modernization

**`_assets/site.js` uses jQuery extensively**
- **Issue**: jQuery 3.4.1 and Bootstrap 4 are outdated
- **Recommendation**: 
  - Consider Bootstrap 5 (drops jQuery dependency)
  - Migrate to vanilla ES6+ JavaScript for better performance
  - Example: Replace `$(...).on("click", ...)` with `addEventListener`

**Inline event handlers in templates**
- **Issue**: `js-scroll-trigger` class used for scroll behavior
- **Recommendation**: Decouple behavior from markup; use data attributes instead

#### 3. HTML Template Issues

**Duplicate IDs in generated HTML (index.html lines 176-228)**
- The `team.html` include uses IDs without proper namespacing
- **Issue**: Multiple pages may have conflicting IDs
- **Fix**: Use unique IDs or remove redundant ID attributes

**Unclosed `<li>` tags in nav.html (line 17-26)**
- Liquid logic correctly handles this, but the `else` branch (line 23) creates a link with `href="#"` with no explicit purpose

#### 4. SCSS/CSS Issues

**Redundant `!important` in button styles (`_assets/components/_buttons.scss`)**
- Overuse of `!important` makes maintenance difficult
- Inconsistent with the cleaner approach in `_services.scss`

**Missing `@mixin heading-font` definition**
- Line 15 in `_buttons.scss` references `heading-font` mixin that may not exist in scope

**Unused CSS files in dist folders**
- `_assets/layout/dist/` and `_assets/components/dist/` contain compiled CSS files alongside source SCSS
- **Recommendation**: Add these to `.gitignore` or clean them up

#### 5. Configuration Issues

**`_config.yml` - Inconsistent URLs**
- Line 3: Refers to "Durban and KZN"
- Line 6-7: Refers to "Cape Town" and "Western Cape"
- **Issue**: Content mismatch
- **Fix**: Align location references

**Missing `exclude` entries**
- `_assets/dist/` and compiled bundles should be excluded from Jekyll processing

#### 6. Data File Issues

**`_data/sitetext.yml`**
- Step 5 is missing from the textblock process (jumps from Step 4 to Step 6)
- **Issue**: Content inconsistency
- **Fix**: Add Step 5 or renumber steps

- Typos in `fab fas fa-home` (line 24) - should be `fas fa-home`

#### 7. Build Process Issues

**`package.json`**
- Uses Webpack 4 (current is v5)
- Bootstrap 4.3.1 is outdated (current is v5)
- jQuery 3.4.1 could be updated to 3.x latest

**`webpack.config.js`**
- No development mode configuration
- No source maps for debugging
- No hot reload for development

---

## Architecture Recommendations

### Short-term (Maintainability)

1. **Clean up dist folders** - Remove compiled CSS from repo or add to `.gitignore`
2. **Fix content inconsistencies** in `_config.yml` and `_data/sitetext.yml`
3. **Remove inline JavaScript** in `page.html`
4. **Consolidate button styles** - Choose one approach (MUI-inspired in `_buttons.scss` or custom in `_services.scss`)

### Medium-term (Modernization)

1. **Migrate to Bootstrap 5** - Remove jQuery dependency
2. **Upgrade Webpack to v5** - Better tree-shaking, faster builds
3. **Add development build** - Separate webpack config for dev mode with source maps
4. **Implement linting** - ESLint for JS, stylelint for SCSS

### Long-term (Architecture)

1. **Consider headless CMS** - For easier content management
2. **Add CI/CD workflow** - GitHub Actions for automated deployments
3. **Implement CSP headers** - Security hardening for production

---

## File References

| File | Lines | Notes |
|------|-------|-------|
| `_assets/site.js` | 1-69 | jQuery-based interactions |
| `_assets/site.scss` | 1-68 | Main stylesheet with modular imports |
| `_assets/components/_buttons.scss` | 1-291 | Button component variants |
| `_layouts/page.html` | 6-10 | Inline JS for background styling |
| `_config.yml` | 3, 6 | Location content mismatch |
| `_data/sitetext.yml` | 24, 103 | Missing step 5, typo in icon class |