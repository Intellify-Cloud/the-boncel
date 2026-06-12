# The Bond Cellar - Documentation

This folder contains architectural and technical review documentation for thebondcellar.co.za website.

## Contents

- **[architecture-review.md](./architecture-review.md)** - Full architecture, stack, and code review
- **[technical-standards.md](./technical-standards.md)** - Standards and best practices guide
- **[seo-strategy.md](./seo-strategy.md)** - SEO implementation plan

## Completed SEO Improvements

The following SEO enhancements have been implemented:

- Fixed location consistency in `_config.yml` (Durban, KZN)
- Added `lang: en-ZA` for local language targeting
- Created `_includes/structured-data.html` with FinancialService schema (JSON-LD)
- Added unique meta descriptions and supporting copy to all calculator pages
- Created proper `robots.txt` with sitemap reference
- Added social preview defaults for Open Graph and Twitter card output

## Pending SEO Tasks

- Replace the current social image with a dedicated 1200x630px Open Graph preview image
- Add FAQ schema for calculators where matching FAQ content is visible on-page
- Consider location-specific landing pages for SEO
