# Code Architecture Review: The Bond Cellar

## Executive Summary

The Bond Cellar is a Jekyll-based static website for a bond origination business in South Africa. The codebase has a straightforward static-site architecture with reusable Liquid includes, YAML-driven content, modular SCSS, and a Webpack asset pipeline. The highest-value improvements are configuration correctness, content/data cleanup, build hygiene, and reducing older Bootstrap/jQuery coupling over time.

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

```txt
.
|-- _assets/           # Source assets (SCSS, JS)
|   |-- base/          # Base styles (variables, mixins, page)
|   |-- components/    # Component styles (buttons, navbar)
|   |-- layout/        # Layout styles (services, team, clients, etc.)
|   `-- */dist/        # Compiled/intermediate CSS that should be reviewed
|-- _config.yml        # Jekyll configuration
|-- _includes/         # Reusable HTML partials
|-- _layouts/          # Page layouts (default, home, page, post)
|-- _data/             # YAML data files for content
|-- _site/             # Generated static site output
|-- assets/            # Bundled JS/CSS and static public assets
|-- *.md               # Top-level content pages
|-- package.json       # Webpack/NPM scripts
`-- Gemfile            # Ruby/Jekyll dependencies
```

---

## Code Standards & Best Practices Review

### Strengths

#### 1. Modular SCSS Architecture

- Styles are organized into `base/`, `components/`, and `layout/`.
- Bootstrap variables are overridden before Bootstrap imports in `_assets/site.scss`.
- CSS custom properties are used for shared design tokens.

#### 2. Separation of Concerns

- Content lives mostly in markdown files and `_data/sitetext.yml`.
- Layout composition uses Liquid includes.
- Site-wide settings are centralized in `_config.yml`.
- Compiled browser assets are emitted to `assets/`.

#### 3. Accessibility Features

- Hero and social icons include useful accessibility attributes.
- Decorative icons generally use `aria-hidden`.
- Button styles include `:focus-visible` handling.
- Content sections use semantic headings and sections.

#### 4. Performance Considerations

- Client logos use lazy loading.
- Google Fonts connections use preconnect hints.
- JavaScript and CSS are bundled through Webpack.
- Production mode minifies assets.

---

## Issues & Recommendations

### 1. Configuration and SEO Correctness

#### Canonical Domain Mismatch

`_config.yml` currently sets `url` to `https://evohomeloans.co.za`, while the project appears to be for The Bond Cellar.

- **Impact**: Canonical tags, sitemap URLs, favicon URLs, and social preview URLs can point at the wrong domain.
- **Fix**: Set `url` to the real production domain for The Bond Cellar.
- **Priority**: High

#### Location Content Mismatch

`_config.yml` mixes Durban/KZN in the title with Cape Town/Western Cape in the description.

- **Impact**: Search metadata, local SEO, and user expectations conflict.
- **Fix**: Pick the correct primary location strategy and align `title`, `description`, schema, visible copy, and sitemap metadata.
- **Priority**: High

#### Analytics Placeholder

`_config.yml` uses `analytics.google: G-XXX`.

- **Impact**: Production measurement will not work if the placeholder ships.
- **Fix**: Replace with the real GA4 measurement ID in production config, or omit analytics when no valid ID is configured.
- **Priority**: Medium
- **Note**: This is a configuration quality issue, not a secret-management concern.

### 2. HTML and Layout Issues

#### Inline JavaScript in `page.html`

`_layouts/page.html` uses inline JavaScript to add `bg-light` to the body for grey pages.

```html
<script>
document.getElementById("page-top").className="bg-light";
</script>
```

- **Impact**: Makes a future Content Security Policy harder to implement and uses JavaScript for a layout concern.
- **Fix**: Add the body class through Liquid in `_layouts/default.html`, or render a page-level wrapper class and style it with CSS.
- **Priority**: Medium

#### Fallback Navigation Links Use `href="#"`

`_includes/nav.html` has a fallback branch that renders links with `href="#"` when neither `url` nor `section` is present.

- **Impact**: Creates no-op links if navigation data is incomplete.
- **Fix**: Validate navigation data or skip rendering links with no destination.
- **Priority**: Low

### 3. JavaScript Modernization

#### jQuery and Bootstrap 4 Coupling

`_assets/site.js` uses jQuery for scrolling, scrollspy, collapse behavior, fade animations, and the back-to-top button. Bootstrap 4 also depends on jQuery and Popper.

- **Impact**: Larger dependency surface and older frontend stack.
- **Fix**: Keep current behavior stable short term. Medium term, consider Bootstrap 5 and vanilla JavaScript replacements.
- **Priority**: Medium

#### Behavior Coupled to Styling Classes

The `js-scroll-trigger` class is used to attach behavior to links.

- **Impact**: Styling/markup classes and JavaScript behavior are coupled.
- **Fix**: Prefer `data-*` attributes for JavaScript hooks during future cleanup.
- **Priority**: Low

### 4. SCSS and Asset Hygiene

#### Compiled CSS in `_assets/**/dist`

The repo contains `dist` directories under `_assets/`, including `_assets/dist`, `_assets/base/dist`, `_assets/components/dist`, and `_assets/layout/dist`.

- **Impact**: Source and generated/intermediate files are mixed, which makes reviews and maintenance noisier.
- **Fix**: Confirm whether these files are used. If not, remove them and add the relevant `_assets/**/dist/` pattern to `.gitignore`.
- **Priority**: Medium

#### `heading-font` Mixin Dependency

`_assets/components/_buttons.scss` includes `@include heading-font;`.

- **Impact**: This is valid only if `_assets/base/mixins` continues to define the mixin and is imported before buttons.
- **Fix**: Keep import order covered by tests/build checks; avoid moving `components/buttons` above `base/mixins`.
- **Priority**: Low

### 5. Data and Content Issues

#### Missing Step 5

`_data/sitetext.yml` jumps from Step 4 to Step 6 in the `textblock` process.

- **Impact**: Visible content appears incomplete or careless.
- **Fix**: Add Step 5 or renumber the sequence.
- **Priority**: Medium

#### Icon Class Typo

The Bond Origination service uses `fas fas fa-home`.

- **Impact**: Redundant class is harmless but sloppy.
- **Fix**: Change to `fas fa-home`.
- **Priority**: Low

#### Encoding Artifacts in Content

Some content contains mojibake where punctuation such as en dashes or em dashes has been rendered as corrupted byte sequences.

- **Impact**: Users may see corrupted punctuation depending on render path/source handling.
- **Fix**: Normalize affected markdown/YAML/docs to UTF-8 and replace corrupted characters with normal ASCII punctuation or valid UTF-8 punctuation consistently.
- **Priority**: Medium

### 6. Build Process Issues

#### Production-Only Webpack Config

`webpack.config.js` hardcodes `mode: 'production'`.

- **Impact**: Local debugging is harder because there are no source maps or dev-oriented build settings.
- **Fix**: Add a development script/config with `mode: 'development'` and source maps.
- **Priority**: Medium

#### Outdated Frontend Tooling

The project uses Webpack 4, Bootstrap 4.3.1, jQuery 3.4.1, and FontAwesome 5.9.0.

- **Impact**: Older dependencies increase maintenance burden and may carry avoidable security or compatibility issues.
- **Fix**: Upgrade incrementally. Start with patch/minor updates that preserve behavior, then plan Bootstrap 5/Webpack 5 as a larger migration.
- **Priority**: Medium

#### Missing Linting and CI Checks

There are no obvious lint/test scripts in `package.json`.

- **Impact**: Regressions in Liquid, SCSS, JS, and generated metadata are easier to miss.
- **Fix**: Add basic build verification first, then ESLint/stylelint/HTML checks if the project will keep evolving.
- **Priority**: Low to Medium

---

## Architecture Recommendations

### Short-Term

1. Fix `_config.yml` domain and location metadata.
2. Clean content issues in `_data/sitetext.yml`, including Step 5 and `fas fas fa-home`.
3. Remove the inline body-class JavaScript from `_layouts/page.html`.
4. Decide whether `_assets/**/dist/` files are source artifacts or generated output, then clean or ignore them.
5. Add a basic build verification step to catch broken imports and generated HTML issues.

### Medium-Term

1. Add a development Webpack mode with source maps.
2. Update jQuery and Bootstrap 4 dependencies within the current architecture.
3. Migrate scroll/back-to-top behavior toward vanilla JavaScript.
4. Add linting for JavaScript and SCSS.
5. Add validation for generated SEO output, especially canonical URLs and sitemap URLs.

### Long-Term

1. Plan a Bootstrap 5 migration to remove the jQuery dependency.
2. Upgrade to Webpack 5 or consider a simpler build tool if the asset pipeline remains small.
3. Add CI/CD checks for build, lint, and deployment.
4. Implement CSP headers after inline scripts are removed.
5. Consider a CMS only if non-developers need frequent content updates.

---

## File References

| File | Lines | Notes |
|------|-------|-------|
| `_config.yml` | 3, 6, 35 | Location mismatch and canonical domain risk |
| `_assets/site.js` | 1-69 | jQuery-based interactions |
| `_assets/site.scss` | 24-40 | Bootstrap imports and SCSS import order |
| `_assets/components/_buttons.scss` | 15 | Depends on `heading-font` mixin |
| `_layouts/page.html` | 6-10 | Inline JS for background styling |
| `_includes/nav.html` | 22-23 | Fallback no-op navigation link |
| `_data/sitetext.yml` | 24, 95-105 | Icon typo and missing Step 5 |
| `webpack.config.js` | 5 | Production-only Webpack mode |
| `.gitignore` | 1-9 | Does not ignore `_assets/**/dist/` |
