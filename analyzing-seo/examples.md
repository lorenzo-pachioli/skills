# SEO Analysis Examples

This file provides real-world examples of SEO implementations to guide your analysis.

## Example 1: Title & Meta Description

### Bad Implementation

```html
<!-- Too generic, no branding, no summary -->
<title>Products</title>
<meta name="description" content="List of all our products." />
```

### Good Implementation

```html
<!-- Descriptive, brand included, succinct summary -->
<title>Gourmet Coffee Beans | Sustainable Flavors - The Bean Roast</title>
<meta
  name="description"
  content="Explore our hand-picked collection of organic, fair-trade coffee beans. From light to dark roast, find your perfect cup today."
/>
```

---

## Example 2: Heading Structure

### Bad Implementation

```html
<!-- Chaotic hierarchy, missing H1, styling instead of semantics -->
<div class="large-text">Welcome to My Site</div>
<h3>Latest News</h3>
<h3>Our Mission</h3>
<h2>Contact Us</h2>
```

### Good Implementation

```html
<!-- Logical, semantic hierarchy -->
<h1>The Bean Roast: Your Guide to Specialty Coffee</h1>
<p>Introductory text about the brand.</p>

<h2>Sustainable Sourcing</h2>
<p>Details about sourcing...</p>

<h3>Direct Trade Relations</h3>
<p>Details about trade...</p>

<h2>Our Brewing Guides</h2>
<p>Links to guides...</p>
```

---

## Example 3: Descriptive URLs

### Bad URLs

- `https://example.com/item.php?id=89234`
- `https://example.com/2024/01/21/category/subcategory/post_1` (too deep/nested)

### Good URLs

- `https://example.com/coffee-beans/espresso-roast`
- `https://example.com/guides/how-to-brew-v60`

---

## Example 4: Image Optimization

### Bad Implementation

```html
<!-- No alt text, generic filename -->
<img src="/assets/img823.png" />
```

### Good Implementation

```html
<!-- Descriptive filename, meaningful alt text -->
<img
  src="/assets/dark-roast-coffee-bag.png"
  alt="A bag of The Bean Roast dark roast espresso coffee beans on a wooden table"
/>
```

---

## Example 5: Structured Data (JSON-LD)

```json
{
  "@context": "https://schema.org",
  "@type": "Product",
  "name": "Organic Sumatra Dark Roast",
  "image": "https://example.com/sumatra.jpg",
  "description": "Earthy and heavy-bodied dark roast with low acidity.",
  "offers": {
    "@type": "Offer",
    "priceCurrency": "USD",
    "price": "18.00",
    "availability": "https://schema.org/InStock"
  }
}
```
