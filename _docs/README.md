# The Bond Cellar - Documentation

This folder contains architectural and technical review documentation for thebondcellar.co.za website.

## Contents

- **[architecture-review.md](./architecture-review.md)** - Full architecture, stack, and code review
- **[technical-standards.md](./technical-standards.md)** - Standards and best practices guide

## Quick Summary

### Tech Stack
- **Static Site Generator**: Jekyll 4.x
- **CSS Framework**: Bootstrap 4.3.1
- **JavaScript**: jQuery 3.4.1 + Bootstrap JS
- **Build**: Webpack 4

### Key Recommendations

1. **Migrate to Bootstrap 5** to eliminate jQuery dependency
2. **Fix content inconsistencies** in `_config.yml` (Durban vs Cape Town references)
3. **Remove inline JavaScript** in `_layouts/page.html`
4. **Clean up dist folders** - they should not be committed
5. **Update missing Step 5** in `_data/sitetext.yml`
6. **Add ESLint/stylelint** for code quality enforcement
7. **Add development webpack config** with source maps

### Strengths
- Excellent modular SCSS architecture
- Proper use of CSS custom properties for design tokens
- Good accessibility baseline
- Clean separation between content and presentation