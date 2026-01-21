# SEO Analysis Reference

This document provides detailed technical requirements and expanded checklists for the `analyzing-seo` skill.

## 1. Discovery & Indexing Details

### Robots.txt Best Practices

- Location: Always at the root (e.g., `https://example.com/robots.txt`).
- Syntax: `User-agent: *` followed by `Disallow: /private/`.
- Sitemaps: Include a link like `Sitemap: https://example.com/sitemap.xml`.

### Canonicalization

- Purpose: Prevent duplicate content issues.
- Implementation: `<link rel="canonical" href="https://example.com/main-page" />` in the `<head>`.
- Use when: The same content is accessible via different URLs (e.g., with/without parameters).

## 2. Technical SEO Checklist

| Feature             | Requirement                                              | Why it matters                  |
| :------------------ | :------------------------------------------------------- | :------------------------------ |
| **HTTPS**           | Every page must use SSL.                                 | Security and ranking signal.    |
| **Mobile UX**       | Google uses Mobile-First Indexing.                       | Most users search on mobile.    |
| **Core Web Vitals** | LCP, FID (or INP), CLS must be within "Good" thresholds. | User experience and ranking.    |
| **Alt Text**        | `alt` attribute should describe the image content.       | Accessibility and Image Search. |

## 3. Writing for Search Appearance

### Good Title Tags

- Length: Typically under 60 characters to avoid truncation.
- Brand: Include the site name (e.g., "Product Name | Site Name").
- Pattern: `Primary Keyword - Secondary Keyword | Brand Name`.

### Good Meta Descriptions

- Length: Typically 150-160 characters.
- Action: Include a call to action (e.g., "Learn more," "Get started").
- Value: Summarize the unique value proposition of the page.

## 4. Semantic HTML Guidelines

- **H1:** The "title" of the content. One per page.
- **H2-H6:** Subheadings. Don't skip levels (e.g., H2 to H4).
- **Links:** Use `<a href="...">` instead of button clicks for navigation whenever possible.
- **Lists:** Use `<ul>`/`<li>` for grouping related items.

## 5. Structured Data (Schema.org)

Common types to implement:

- **Article:** For blog posts or news.
- **Product:** For e-commerce pages.
- **Organization:** For the brand identity.
- **FAQPage:** For frequently asked questions.
- **BreadcrumbList:** To influence search result breadcrumbs.

## 6. Anti-Patterns to Avoid

- ❌ **Keyword Stuffing:** Artificially inflating keyword frequency.
- ❌ **Hidden Text:** Hiding text from users but showing it to bots.
- ❌ **Intrusive Interstitials:** Pop-ups that block main content on mobile.
- ❌ **Internal "NoFollow":** Don't use `rel="nofollow"` on your own internal links unless necessary.
- ❌ **Thin Content:** Pages with very little text or value.
