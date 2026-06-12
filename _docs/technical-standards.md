# Technical Standards & Best Practices

## JavaScript Standards

### Current State

- jQuery is used for scroll behavior, Bootstrap 4 collapse/scrollspy, and the back-to-top button.
- Webpack builds a production bundle from `_assets/bundle.js`.
- There is no linting configuration or explicit transpilation target.
- Inline scripts still exist in `_includes/head.html` and `_layouts/page.html`.

### Recommended Patterns

Prefer vanilla JavaScript for new behavior where it does not force a broad Bootstrap 4 migration.

```javascript
document.addEventListener('DOMContentLoaded', () => {
  document.querySelectorAll('[data-scroll-trigger]').forEach((element) => {
    element.addEventListener('click', handler);
  });
});
```

### Naming Conventions

- Existing `js-` classes are acceptable for current behavior.
- Prefer `data-*` attributes for new JavaScript hooks and configuration.
- Keep behavior hooks separate from visual styling classes when touching templates.

---

## SCSS/CSS Standards

### File Organization

```txt
_assets/
|-- base/          # _variables.scss, _mixins.scss, _page.scss
|-- components/    # _buttons.scss, _navbar.scss
|-- layout/        # Section-specific styles
`-- **/dist/       # Generated/intermediate CSS; review before keeping
```

### Style Guide

| Element | Current | Standard |
|---------|---------|----------|
| Colors | CSS custom properties + Bootstrap variables | Keep both while Bootstrap 4 is in place; document shared tokens in `_assets/site.scss` |
| Spacing | Mix of `rem` and `px` | Prefer `rem` for new spacing, use `px` only for fixed assets or borders |
| Breakpoints | Bootstrap defaults | Use Bootstrap breakpoints unless a section has a documented reason |
| Mixins | Defined in `_assets/base/_mixins.scss` | Keep `base/mixins` imported before component partials |

### CSS Custom Properties

Use shared design tokens for cross-section colors:

```scss
:root {
  --color-header: #021736;
  --color-section-bg: #F8F9FA;
}
```

### Inline Styles

Avoid adding new inline styles in Liquid or Markdown templates. Existing inline styles should be migrated to SCSS when touching the relevant component.

---

## Jekyll/Liquid Standards

### Correct Implementations

- Use `relative_url` for site-relative asset paths.
- Keep reusable markup in `_includes`.
- Keep page shells in `_layouts`.
- Keep site text and repeated content in `_data/sitetext.yml`.
- Use `default` filters for optional data values.

```liquid
{{ site.data.sitetext.about.section | default: 'about' }}
```

### Template Rules

- Avoid no-op links such as `href="#"` unless they are intentionally wired to behavior.
- Avoid inline JavaScript in layouts and includes.
- Ensure includes fail gracefully when optional data is missing.
- Do not add third-party form endpoints without documenting the provider and spam/privacy handling.

---

## Contact and Forms

### Current Standard

The site does not use Formspree and should not include Formspree-specific code.

Do not add:

- `https://formspree.io/...` form actions
- Formspree `_replyto`, `_gotcha`, `_next`, or `_subject` hidden fields
- Dead contact forms with no backend

Use direct contact actions instead:

- `tel:` links for phone calls
- `mailto:` links for email
- WhatsApp links only when explicitly desired, with `target="_blank"` and `rel="noopener noreferrer"`

If a contact form is added later, choose and document the backend first, then add accessible labels, spam protection, privacy copy, and success/error states.

---

## Git and VCS Standards

### Current State

- `.gitignore` already excludes `node_modules`, `.jekyll-cache`, `_site`, and other local artifacts.
- `.editorconfig`, `.prettierrc`, ESLint, and stylelint are not configured.
- `assets/bundle.js` and `assets/bundle.css` are currently referenced by the site and may be deployable outputs.

### Recommended `.gitignore` Review

Do not ignore `assets/bundle.*` unless deployment is changed to build assets during CI/deploy.

Review whether these generated/intermediate folders should be ignored:

```gitignore
_assets/**/dist/
```

---

## Security Guidelines

### Current Issues

1. Inline JavaScript makes a strict Content Security Policy difficult.
2. Google Analytics is loaded from an external script.
3. Some links that open a new tab should be checked for `rel="noopener noreferrer"`.
4. There is no documented CSP target.

### Recommendations

- Remove inline scripts before enforcing a strict CSP.
- Prefer CSP allowlists over SRI for Google Analytics, because the external analytics script can change.
- Keep `rel="noopener noreferrer"` on all `target="_blank"` links.
- Do not include unused third-party form services.

Example future CSP direction after inline scripts are removed:

```yaml
webserver_headers:
  - - Content-Security-Policy
    - "default-src 'self'; script-src 'self' https://www.googletagmanager.com; connect-src 'self' https://www.google-analytics.com; img-src 'self' data: https:; style-src 'self' https://fonts.googleapis.com; font-src 'self' https://fonts.gstatic.com"
```

---

## Performance Guidelines

### Already Implemented

- Google Fonts preconnect hints.
- Lazy loading on client logos.
- Bundle minification through Terser and optimize-css-assets.

### Missing or Worth Reviewing

- Responsive image sets with `srcset`.
- Asset versioning or hashed output for cache busting.
- Development source maps for easier debugging.
- Critical CSS only if performance audits show render-blocking CSS is a real issue.
- Service worker only if offline support or app-like behavior becomes a real requirement.

---

## Accessibility Checklist

| Criterion | Status | Notes |
|-----------|--------|-------|
| Semantic HTML | Partial | Header/nav/footer exist; add a `main` landmark if practical |
| Image alt text | Partial | Many images have alt text, but generic/empty alt values need an audit |
| ARIA labels | Partial | Hero and controls have labels in places |
| Focus management | Partial | Button focus styles exist |
| Color contrast | Review | Gold on navy should be checked with a contrast tool |
| Skip navigation | Missing | Add a skip link for keyboard users |
| Form labels | N/A | No backend contact form should be present while Formspree is not used |

---

## SEO Recommendations

### Current

- `jekyll-seo-tag` plugin installed.
- `jekyll-sitemap` plugin installed.
- Meta viewport configured.
- Canonical URLs generated from `_config.yml`.

### Missing or In Progress

- Correct production `url` in `_config.yml`.
- Consistent Durban/KZN vs Cape Town/Western Cape metadata.
- Open Graph image configuration.
- Twitter card configuration.
- Organization/local business structured data.
- Unique descriptions for calculator pages.
