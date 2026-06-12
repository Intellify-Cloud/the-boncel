# Technical Standards & Best Practices

## JavaScript Standards

### Current State
- ES5-compatible jQuery patterns
- No modules, no transpilation target specified
- No linting configuration

### Recommended Patterns

```javascript
// Instead of jQuery event handlers
$(document).ready(function() {
  $('.js-scroll-trigger').on('click', handler);
});

// Use vanilla ES6+
document.addEventListener('DOMContentLoaded', () => {
  document.querySelectorAll('.js-scroll-trigger').forEach(el => {
    el.addEventListener('click', handler);
  });
});
```

### Naming Conventions
- Use `js-` prefix for JavaScript hooks (correctly implemented)
- Use `data-` attributes for configuration (not implemented)

---

## SCSS/CSS Standards

### File Organization
```
_assets/
├── base/          # _variables.scss, _mixins.scss, _page.scss
├── components/    # _buttons.scss, _navbar.scss
└── layout/        # Section-specific styles
```

### Style Guide Compliance

| Element | Current | Recommendation |
|---------|---------|--------------|
| Colors | CSS vars + Bootstrap vars | Standardize on one approach |
| Spacing | Mix of rem and px | Use consistent rem units |
| Breakpoints | Bootstrap defaults | Document custom breakpoint usage |

### CSS Custom Properties (Correctly Used)
```scss
:root {
  --color-header: #021736;
  --color-section-bg: #F8F9FA;
  // ...
}
```

### Mixin Usage (Incomplete)
```scss
// _assets/base/_mixins.scss should define heading-font
@mixin heading-font {
  font-family: 'Roboto', 'Helvetica', 'Arial', sans-serif;
  font-weight: 700;
}
```

---

## Jekyll/Liquid Standards

### Correct Implementations
- Use of `relative_url` filter for asset paths
- Collection configuration for portfolio
- SEO plugin integration

### Anti-patterns Found
```liquid
// Avoid: Inline styling in templates
style="background-color:#021736"

// Prefer: CSS classes
class="navbar-dark bg-primary"
```

### Include Best Practices
- Ensure all includes check for existence of variables
- Use `default` filter for optional values:
```liquid
{{ site.data.sitetext.about.section | default: 'hero' }}
```

---

## Git/H VCS Standards

### Missing Configuration
- No `.gitignore` for `node_modules/`, `assets/bundle.*`
- No `.editorconfig` for consistent formatting
- No `.prettierrc` or similar formatter config

### Recommended .gitignore Entries
```
# Build outputs
/assets/bundle.js
/assets/bundle.css

# Node
node_modules/

# Dist folders (should be in .gitignore)
_assets/layout/dist/
_assets/components/dist/
```

---

## Security Guidelines

### Current Issues
1. Inline JavaScript without CSP nonce support
2. External scripts (Google Analytics) loaded without integrity attributes
3. Forms would need CAPTCHA/reCAPTCHA (not present in static site)
4. WhatsApp and social links open in new tab with `target="_blank"` without `rel="noopener noreferrer"` (partially implemented)

### Recommendations
- Add SRI hashes for external scripts
- Implement CSP headers via `_config.yml`:
```yaml
webserver_headers:
  - - Content-Security-Policy
    - "default-src 'self'; script-src 'self' 'unsafe-inline' www.googletagmanager.com"
```

---

## Performance Guidelines

### Already Implemented
- Font preloading with `preconnect`
- Image lazy loading on client logos
- Bundle minification via Terser/optimize-css-assets

### Missing Optimizations
- No responsive image sets (`srcset`)
- No critical CSS inlining
- No service worker registration
- No asset versioning for cache busting

---

## Accessibility Checklist

| Criterion | Status | Notes |
|-----------|--------|-------|
| Semantic HTML | ✅ | Proper header/nav/main/footer structure |
| Image alt text | ✅ | All images have alt attributes |
| ARIA labels | ✅ | Hero section labeled |
| Focus management | ✅ | Button focus styles present |
| Color contrast | ⚠️ | Gold (#BA9A49) on navy (#021736) may need checking |
| Skip navigation | ❌ | No skip link for keyboard users |
| Form labels | N/A | No forms implemented |

---

## SEO Recommendations

### Current
- jekyll-seo-tag plugin installed
- Meta viewport configured
- Canonical URLs generated

### Missing
- Open Graph image specification
- Twitter card sizing
- Structured data for organization/local business