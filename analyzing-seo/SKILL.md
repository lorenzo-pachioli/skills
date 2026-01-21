---
name: analyzing-seo
description: Analyze and optimize frontend projects for SEO based on Google Search Central guidelines. Use when evaluating a website's search visibility, content quality, and technical health. Covers crawling, site structure, content, and appearance in search results.
---

# Analyzing SEO

This skill provides a systematic workflow for analyzing and improving the Search Engine Optimization (SEO) of frontend projects, following the official [Google SEO Starter Guide](https://developers.google.com/search/docs/fundamentals/seo-starter-guide).

## When to Use

- When asked to "analyze the SEO" of a project or specific page.
- During the development of new landing pages or site sections.
- When troubleshooting why a page is not appearing in Google Search.
- When refactoring frontend code to improve semantic structure and visibility.

## Quick Reference

- **Title Link:** The headline shown in search results, influenced by `<title>` and `<h1>`.
- **Snippet:** The description below the title, often sourced from the `<meta name="description">`.
- **Crawling:** The process where search engine bots discover your pages.
- **Indexing:** The process where discovered pages are processed and stored in the search index.
- **Canonical URL:** The preferred version of a page when duplicate content exists.

## Workflow

### Step 1: Discovery & Visibility Analysis

Check if search engines can find and access the content.

- [ ] **Search Operator Check:** Use `site:yourdomain.com` in Google to see what is currently indexed.
- [ ] **Robots.txt:** Verify if `robots.txt` is blocking important pages.
- [ ] **Sitemap:** Ensure a `sitemap.xml` exists and is linked in `robots.txt`.
- [ ] **Crawlability:** Check if essential resources (CSS, JS) are accessible to crawlers.

### Step 2: Content & Structure Analysis

Evaluate the value and organization of the information.

- [ ] **Descriptive URLs:** Ensure URLs are human-readable and use words instead of IDs (e.g., `/pets/cats` instead of `/p/123`).
- [ ] **Semantic Headings:** Use a single `<h1>` for the main topic and nested headings (`<h2>`, `<h3>`) logically.
- [ ] **Content Quality:** Verify content is unique, helpful, reliable, and "people-first".
- [ ] **Internal Linking:** Ensure pages are connected via crawlable `<a>` tags with descriptive anchor text.

### Step 3: Influence Search Appearance

Optimize how the site looks in search results.

- [ ] **Title Tags:** unique, clear, and concise `<title>` elements for every page.
- [ ] **Meta Descriptions:** Succinct summaries that encourage clicks.
- [ ] **Structured Data:** Use [Schema.org](https://schema.org) markup to enable rich results (reviews, carousels, FAQs).

### Step 4: Asset Optimization

Ensure non-text elements are contributing to SEO.

- [ ] **Image Alt Text:** Descriptive alt tags for all meaningful images.
- [ ] **Video Metadata:** Descriptive titles and descriptions for embedded videos.
- [ ] **Mobile-Friendliness:** Ensure the site is responsive and performs well on mobile devices.

### Step 5: Verification & Monitoring

Final checks and ongoing improvement.

- [ ] **Search Console:** Recommend setting up Google Search Console for performance tracking.
- [ ] **URL Inspection:** Use Search Console's URL Inspection tool to see how Google renders specific pages.

## Additional Resources

- **[reference.md](reference.md)** - Detailed checklists and technical requirements.
- **[examples.md](examples.md)** - Before/after comparisons and best practices.

---

**Remember:** Content quality is the most significant factor. Focus on creating value for users first, then optimize for search engines.
