# SEO Guide for Coding Agents

## Purpose

This guide is for small public-facing marketing microsites, typically:

```text
1–30 pages
```

The goal is:

> Build websites that are easy for people, Google, and AI search systems to find, understand, trust, and use.

Keep SEO simple.

Do the fundamentals exceptionally well.

---

# 1. Core Principles

Always prioritise:

* useful, people-first content
* clear site structure
* semantic HTML
* crawlable links
* fast pages
* excellent mobile UX
* accurate business information
* accessibility
* simple maintainable code

Never use:

* keyword stuffing
* hidden text
* fake reviews
* fake structured data
* doorway/location spam
* mass-generated low-value AI content
* SEO tricks intended primarily to manipulate rankings

A useful test:

> Would this page still be valuable if Google did not exist?

If not, improve the page.

---

# 2. How Search Works

Think about every page in this order:

```text
DISCOVER
   ↓
CRAWL
   ↓
INDEX
   ↓
UNDERSTAND
   ↓
RANK
   ↓
SEARCH APPEARANCE
   ↓
VISITOR
```

Before trying to improve rankings, make sure Google can:

1. find the page
2. crawl it
3. index it
4. understand it

---

# 3. Site Architecture

Keep microsite architecture simple.

Example:

```text
/
├── about/
├── services/
│   ├── service-a/
│   └── service-b/
├── projects/
├── faq/
└── contact/
```

Every important page should be reachable through normal navigation or contextual internal links.

Avoid orphan pages.

Do not create unnecessary layers of navigation.

---

# 4. URLs

Use clean, descriptive URLs.

Good:

```text
/services/home-loans/
```

Bad:

```text
/page?id=38291
```

Prefer:

```text
lowercase
hyphens
short descriptive paths
stable URLs
```

Avoid unnecessary:

```text
parameters
IDs
dates
tracking information
```

in canonical URLs.

Do not change an established URL without a reason.

If a page genuinely moves:

```text
OLD URL
   ↓
301 / 308
   ↓
NEW URL
```

---

# 5. Canonical URLs

A canonical tells Google:

> This is the preferred official URL for this page.

Every normal indexable microsite page should generally have a self-referencing canonical.

Page:

```text
https://example.co.za/services/home-loans/
```

Canonical:

```html
<link
  rel="canonical"
  href="https://example.co.za/services/home-loans/"
>
```

This also helps when URLs gain tracking parameters.

For example:

```text
https://example.co.za/services/home-loans/?utm_source=facebook
```

should still canonicalise to:

```text
https://example.co.za/services/home-loans/
```

Keep these aligned:

```text
PAGE URL
   ↓
CANONICAL
   ↓
INTERNAL LINKS
   ↓
SITEMAP
   ↓
STRUCTURED DATA
   ↓
OPEN GRAPH URL
```

They should normally point to the same preferred URL.

### Canonical vs Redirect

Use:

```text
duplicate/variant URL
→ canonical
```

Use:

```text
page permanently moved
→ 301/308 redirect
```

### Canonical vs Noindex

```text
canonical
= this is the preferred version
```

```text
noindex
= do not include this page in Search
```

Do not confuse them.

---

# 6. Crawlable Links

Navigation must use real links.

Good:

```html
<a href="/services/">Services</a>
```

Avoid using JavaScript-only navigation when a normal link is appropriate.

Rule:

```text
NAVIGATION
→ <a>

ACTION
→ <button>
```

Use descriptive anchor text.

Good:

```text
home loan application process
```

Weak:

```text
click here
```

---

# 7. Page Titles

Every important page needs a unique `<title>`.

Good:

```html
<title>Home Loans in Durban | Brand Name</title>
```

Weak:

```html
<title>Home</title>
```

Useful patterns:

```text
Page Subject | Brand
```

or where genuinely relevant:

```text
Service in Location | Brand
```

Titles should be:

* descriptive
* natural
* accurate
* unique

Do not keyword stuff.

Do not optimise against an arbitrary character count.

Google may rewrite the displayed title.

---

# 8. Meta Descriptions

Give important pages useful unique descriptions.

Example:

```html
<meta
  name="description"
  content="Expert home loan guidance, bank comparisons and application support."
>
```

Descriptions should:

* accurately summarise the page
* communicate value
* match search intent
* sound natural
* encourage the right visitor

Do not use keyword lists.

There is no magic 155/160-character requirement.

Google may generate a different snippet.

That is normal.

---

# 9. Valid Page Metadata

Keep `<head>` clean and valid.

Typical structure:

```html
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">

  <title>...</title>
  <meta name="description" content="...">

  <link rel="canonical" href="...">
  <link rel="icon" href="/favicon.png">

  <!-- Social metadata -->
  <!-- Structured data -->
  <!-- CSS/scripts -->
</head>
```

Do not place normal body content inside `<head>`.

Never put elements such as:

```text
<img>
<iframe>
<h1>
<section>
<div>
```

inside `<head>`.

Invalid markup can interfere with Google's processing of metadata that follows it.

Also avoid duplicate:

```text
<title>
description
canonical
robots
```

metadata.

Centralise `<head>` generation wherever possible.

---

# 10. Headings

Use headings to describe document structure.

Example:

```text
H1 Home Loans

  H2 How We Help

    H3 First-Time Buyers

    H3 Property Investors

  H2 How It Works

  H2 Frequently Asked Questions
```

Normally use one clear primary H1.

Do not choose heading levels based on visual size.

Use CSS for presentation.

---

# 11. Content

Every page should answer:

```text
Who is this for?

What problem does it solve?

What does the visitor need to know?

Why should they trust this business?

What should they do next?
```

Prefer:

* real expertise
* real examples
* original information
* clear explanations
* local knowledge
* actual projects
* case studies
* genuine photographs
* useful FAQs

Avoid filler written merely to make pages longer.

There is no required SEO word count.

---

# 12. AI-Generated Content

AI can help with:

* drafting
* editing
* research
* structure
* metadata
* summarisation
* ideas

But the preferred workflow is:

```text
REAL BUSINESS KNOWLEDGE
        ↓
AI ASSISTANCE
        ↓
FACT CHECK
        ↓
HUMAN / AGENT REVIEW
        ↓
PUBLISH
```

Never allow AI to invent:

* testimonials
* customers
* statistics
* qualifications
* prices
* awards
* business locations
* case studies
* citations
* ratings

Do not mass-produce pages simply to target search queries.

---

# 13. Keywords

Use words customers naturally use.

Do not optimise for keyword density.

Do not repeatedly force exact-match phrases into content.

Use:

```text
primary topic
related concepts
natural synonyms
questions customers ask
industry terminology
location where genuinely relevant
```

Do not use:

```html
<meta name="keywords">
```

for Google SEO.

---

# 14. Internal Linking

Important pages should receive useful internal links.

Example:

```html
Learn more about our
<a href="/services/home-loans/">
  home loan application service
</a>.
```

Internal links help:

```text
users
Google discovery
site structure
page relationships
importance
```

Do not rely only on the sitemap to expose important pages.

---

# 15. Images

Important images should:

* be relevant
* load quickly
* use sensible dimensions
* have descriptive filenames
* appear near relevant content
* use responsive delivery where appropriate

Example:

```html
<img
  src="/assets/img/home-loan-consultation.webp"
  alt="Home loan adviser meeting with a client"
  width="1200"
  height="800"
>
```

Do not place important information only inside an image.

---

# 16. Alt Text

Use useful alt text for meaningful images.

Good:

```html
alt="Amanda Strydom, Property Finance Specialist"
```

Bad:

```html
alt="image"
```

Bad:

```html
alt="best cheap home loans mortgage Durban finance"
```

Decorative imagery generally uses:

```html
alt=""
```

Accessibility comes first.

---

# 17. Semantic HTML

Prefer:

```html
<header>
<nav>
<main>
<section>
<article>
<footer>
```

Use real:

```html
<a>
<button>
<label>
```

instead of making generic `<div>` elements imitate them.

Semantic HTML improves:

```text
accessibility
SEO
browser behaviour
maintainability
machine understanding
```

---

# 18. robots.txt

For most production microsites:

```text
User-agent: *
Allow: /

Sitemap: https://example.co.za/sitemap.xml
```

That is normally enough.

Do not create complicated crawler rules without a genuine reason.

Do not unnecessarily block:

```text
CSS
JavaScript
images
```

Never accidentally deploy:

```text
User-agent: *
Disallow: /
```

to production.

Treat that as a release blocker.

---

# 19. robots.txt Is Not Security

robots.txt controls crawling.

It does not secure information.

```text
ROBOTS.TXT
= crawl control

NOINDEX
= indexing control

AUTHENTICATION
= access control
```

Sensitive content requires real access protection.

---

# 20. Sitemap

For a ≤30-page microsite use:

```text
/sitemap.xml
```

One sitemap is normally enough.

It should contain the canonical URLs of important public indexable pages.

Include:

```text
200
public
canonical
indexable
production URLs
```

Exclude:

```text
redirects
404s
noindex pages
drafts
staging URLs
private pages
```

Do not normally build:

```text
sitemap indexes
image sitemaps
video sitemaps
news sitemaps
```

for a small marketing site.

---

# 21. Sitemap Dates

Use `<lastmod>` only when accurate.

Do not set every page to today's date simply because the site was rebuilt.

Rule:

```text
accurate lastmod
>
no lastmod
>
fake lastmod
```

Do not spend time on:

```text
changefreq
priority
```

for Google.

---

# 22. Search Appearance

Focus on making the normal Google result excellent:

```text
FAVICON

SITE NAME

TITLE

URL

SNIPPET

IMAGE

BUSINESS IDENTITY
```

Do this before chasing rich results.

Google ultimately decides how a search result appears.

---

# 23. Favicon

Every production microsite needs a favicon.

Example:

```html
<link rel="icon" href="/favicon.png">
```

Use a recognisable brand mark that remains clear at small sizes.

The favicon can appear in Google Search results.

---

# 24. Structured Data

Keep schema simple.

Typical homepage:

```text
WebSite

+

Organization
```

or when appropriate:

```text
WebSite

+

LocalBusiness
```

Conditional:

```text
BreadcrumbList
Article
VideoObject
Event
```

only when the content genuinely warrants it.

Do not schema-stuff.

---

# 25. Structured Data Must Be True

Structured data should describe reality.

```text
VISIBLE REAL INFORMATION
        ↓
STRUCTURED DATA
```

Never:

```text
SEO WISH
   ↓
FAKE SCHEMA
```

Never invent:

```text
reviews
ratings
prices
locations
authors
qualifications
opening hours
offers
```

Passing a schema validator does not guarantee a rich result.

---

# 26. FAQ

FAQ sections remain useful for:

* answering questions
* handling objections
* explaining services
* long-tail content
* conversion

But do not add FAQ schema expecting expandable FAQ Google results.

Build FAQs because they help users.

---

# 27. Local SEO

For local businesses keep these accurate and consistent:

```text
business name
address / service area
telephone
opening hours
website
business category
```

Align the website with Google Business Profile.

Do not create fake location pages.

Avoid:

```text
/home-loans-durban/
/home-loans-kloof/
/home-loans-westville/
/home-loans-pinetown/
```

where the only meaningful difference is the town name.

Location pages need genuine local value.

---

# 28. Performance

Microsites should be fast.

Avoid unnecessary:

```text
huge JavaScript bundles
giant images
multiple font families
unused libraries
heavy animation frameworks
third-party scripts
```

Good Core Web Vitals targets:

```text
LCP ≤ 2.5s
INP < 200ms
CLS < 0.1
```

Do not chase Lighthouse 100 merely for the score.

---

# 29. Hero Performance

The hero often determines LCP.

Therefore:

* compress hero images
* use responsive sizes
* specify dimensions/aspect ratio
* avoid giant source files
* do not lazy-load the primary LCP image

Keep important hero text as actual HTML rather than baking it into an image.

---

# 30. Mobile

Every page must work properly on mobile.

Check:

```text
navigation
font sizes
tap targets
forms
images
spacing
horizontal overflow
modals
CTA buttons
```

Do not hide important content from mobile users.

---

# 31. Search Console

Production sites should use Google Search Console.

Monitor:

```text
search queries
impressions
clicks
pages
indexing
sitemaps
Core Web Vitals
security issues
```

Do not confuse third-party SEO scores with Google ranking scores.

---

# 32. AI Search

Do not create a separate technical SEO system for AI.

Good foundations remain:

```text
USEFUL CONTENT
+
CLEAR ENTITIES
+
SEMANTIC HTML
+
ORIGINAL INFORMATION
+
INTERNAL LINKS
+
IMAGES
+
STRUCTURED DATA
+
NORMAL SEO
```

Do not automatically add:

```text
AI schema
GEO schema
AI keyword density
forced content chunking
special Google AI markup
```

because somebody claims it guarantees AI visibility.

---

# 33. Jekyll Implementation

Centralise SEO.

Use one clear source of truth for shared SEO metadata. A site may use a plugin such as `jekyll-seo-tag`, or it may use local includes such as `seo.html` and `schema.html`, but it should not generate duplicate title, description or canonical tags.

```text
_config.yml

_includes/
├── seo.html
└── schema.html

_layouts/
└── default.html

robots.txt
sitemap.xml
```

For Jekyll, `jekyll-seo-tag` is a good default for title, description, canonical, Open Graph and basic JSON-LD metadata. If a site uses it, add only complementary structured data by hand and avoid duplicating tags it already emits.

Page front matter can provide:

```yaml
---
title:
description:
permalink:
image:
---
```

Generate the canonical from:

```text
production domain
+
page URL
```

For example:

```liquid
<link
  rel="canonical"
  href="{{ page.url | absolute_url }}"
>
```

Do not manually duplicate SEO markup throughout layouts.

---

# 34. Vue Implementation

First identify whether the site uses:

```text
SPA
SSG
SSR
Nuxt
prerendering
```

For public marketing sites prefer SSG, SSR or prerendering where practical.

For every public route verify:

```text
direct URL works
title is correct
description is correct
canonical is correct
H1 exists
content renders
links are crawlable
```

---

# 35. Page Checklist

Every important page should have:

```text
[ ] clear purpose
[ ] clean URL
[ ] unique title
[ ] useful description
[ ] self-referencing canonical
[ ] clear H1
[ ] logical H2/H3 structure
[ ] useful original content
[ ] internal links
[ ] relevant images
[ ] appropriate alt text
[ ] clear CTA
[ ] semantic HTML
[ ] mobile support
[ ] good performance
```

---

# 36. Production Checklist

Before deployment:

```text
[ ] HTTPS works
[ ] production domain correct
[ ] preferred hostname correct

[ ] robots.txt allows crawling
[ ] sitemap.xml works
[ ] sitemap contains production canonical URLs

[ ] no accidental noindex
[ ] canonicals use production domain
[ ] internal links use preferred URLs

[ ] redirects work
[ ] missing pages return 404

[ ] titles correct
[ ] descriptions correct
[ ] H1s correct

[ ] head markup valid
[ ] no duplicate metadata

[ ] navigation works
[ ] images work
[ ] alt text reviewed

[ ] schema is accurate and valid

[ ] mobile works
[ ] performance acceptable

[ ] no major browser console errors
```

---

# 37. SEO Audit Priorities

Classify findings:

### P0 — Critical

```text
site-wide noindex
Disallow: /
wrong-domain canonical
production unavailable
```

### P1 — High

```text
missing titles
broken navigation
broken canonicals
important orphan pages
incorrect redirects
```

### P2 — Improve

```text
weak descriptions
poor internal linking
missing useful alt text
oversized images
weak content
```

### P3 — Nice to Have

```text
minor filename improvements
optional schema
small metadata refinements
```

Do not treat every SEO issue as critical.

---

# 38. Agent Workflow

When asked to review or improve SEO:

```text
1. Understand the business and audience.

2. Map the public pages.

3. Check crawlability and indexability.

4. Check URLs and canonicals.

5. Review titles and descriptions.

6. Review headings and content.

7. Review internal linking.

8. Review images and alt text.

9. Review structured data.

10. Review mobile and performance.

11. Fix P0/P1 issues first.

12. Build the site.

13. Inspect rendered HTML.

14. Verify production.
```

Do not blindly rewrite the entire site.

---

# 39. Agent Reporting

Report findings clearly:

```text
SEO REVIEW

Overall
Good / Needs Work / Critical

P0 — Critical
- ...

P1 — High
- ...

P2 — Improvements
- ...

Implemented
- ...

Recommended Next
- ...
```

Where useful identify:

```text
route
file
problem
change
```

Example:

```text
/services/home-loans/

Problem:
Generic page title.

Change:
Home Loans in Durban | Brand Name
```

---

# 40. Things to Ignore

Do not waste development time on:

```text
meta keywords
keyword density
exact title character counts
exact description character counts

crawl budget for a 20-page site

sitemap priority
sitemap changefreq
sitemap indexes

mass location pages

fake reviews
fake ratings

schema stuffing

AI schema
GEO schema

SEO plugin scores
```

Unless the project has an unusual requirement, these are distractions.

---

# 41. Definition of Done

SEO is in good shape when:

```text
Google can find the pages.

Google can crawl them.

Google can index the intended pages.

URLs are clean.

Canonicals are consistent.

Titles describe the pages.

Content answers real questions.

HTML is semantic.

Internal links make sense.

Images are optimised.

Business information is accurate.

Structured data reflects reality.

Mobile works well.

Pages are fast.

robots.txt is simple and correct.

sitemap.xml is simple and correct.

Production output has been checked.
```

Then stop adding SEO infrastructure.

Improve the actual website.

---

# Golden Rule

For a microsite:

> **Make the website exceptionally easy to understand.**

For:

```text
PEOPLE
SEARCH ENGINES
AI SYSTEMS
BROWSERS
ASSISTIVE TECHNOLOGY
DEVELOPERS
```

Prefer:

```text
simple
semantic
fast
useful
accurate
crawlable
well structured
maintainable
```

over:

```text
complex
over-optimised
keyword-heavy
schema-heavy
plugin-heavy
AI-generated
```

For a 1–30 page microsite, excellent fundamentals are the SEO strategy.
