---
name: seo-and-geo-optimization
description: Apply this skill when editing frontend pages, landing pages, or metadata to ensure maximum visibility on traditional search engines (SEO) and AI-driven search engines (GEO/LLM Search).
---

# SEO & GEO Optimization Guidelines

Use this skill whenever you are modifying, creating, or auditing public-facing pages (especially `index.html`) to optimize them for Google search (SEO) and AI search engines like Gemini, ChatGPT, Perplexity (GEO - Generative Engine Optimization).

## Core Principles

1. **AI-Search Friendly (GEO - Generative Engine Optimization)**:
   * **Explicit Entity Definitions**: State clearly that deGudang is a cozy neighborhood cafe and roastery offering hand-roasted specialty coffee, fresh artisanal pastries, and a warm atmosphere in Lumajang, Jawa Timur. AI crawlers rely on explicit statements rather than implicit marketing jargon.
   * **Structured Data (JSON-LD)**: Always include Schema.org JSON-LD microdata (e.g., `Restaurant`, `WebSite`, `SiteNavigationElement`) to help LLMs parse structured relationships and features.
   * **Citation-Friendly Formats**: Structure text using bullet points, tables, and bold key phrases. AI search engines prefer extracting structured lists and highlighted conclusions.

2. **Traditional SEO (Search Engine Optimization)**:
   * **Semantic HTML**: Use proper HTML5 tags (`<header>`, `<nav>`, `<main>`, `<section>`, `<footer>`). Ensure only one `<h1>` per page.
   * **Metadata & Open Graph**: Provide complete meta titles (under 60 characters), descriptions (under 160 characters), and Open Graph (og) / Twitter tags for social previews.
   * **Fast Loading & Assets**: Optimize images (use modern formats like WebP/AVIF), avoid heavy client-side scripts where static HTML suffices, and implement responsive designs.

## Implementation Checklist

### 1. Metadata Configuration (HTML)
Ensure every public page includes:
```html
<title>deGudang - Cozy Cafe & Roastery</title>
<meta name="description" content="Welcome to deGudang, a cozy neighborhood cafe in Lumajang offering hand-roasted specialty coffee, fresh artisanal pastries, and a warm atmosphere." />

<!-- Open Graph / Facebook -->
<meta property="og:type" content="website" />
<meta property="og:title" content="deGudang - Cozy Cafe & Roastery" />
<meta property="og:description" content="Welcome to deGudang, a cozy neighborhood cafe in Lumajang offering hand-roasted specialty coffee, fresh artisanal pastries, and a warm atmosphere." />
<meta property="og:image" content="/assets/images/degudang.png" />

<!-- Twitter -->
<meta property="twitter:card" content="summary_large_image" />
<meta property="twitter:title" content="deGudang - Cozy Cafe & Roastery" />
<meta property="twitter:description" content="Welcome to deGudang, a cozy neighborhood cafe in Lumajang offering hand-roasted specialty coffee, fresh artisanal pastries, and a warm atmosphere." />
<meta property="twitter:image" content="/assets/images/degudang.png" />
```

### 2. JSON-LD Schema (Place inside `<head>`)
For the main landing page, include a `Restaurant` schema:
```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Restaurant",
  "name": "deGudang Cafe & Roastery",
  "image": "https://degudang.netlify.app/assets/images/degudang.png",
  "@id": "https://degudang.netlify.app",
  "url": "https://degudang.netlify.app",
  "telephone": "+62...",
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "Pulo, Kec. Tempeh",
    "addressLocality": "Lumajang",
    "addressRegion": "Jawa Timur",
    "postalCode": "67371",
    "addressCountry": "ID"
  },
  "geo": {
    "@type": "GeoCoordinates",
    "latitude": -8.1746228,
    "longitude": 113.1559376
  },
  "openingHoursSpecification": [
    {
      "@type": "OpeningHoursSpecification",
      "dayOfWeek": [
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday"
      ],
      "opens": "07:00",
      "closes": "22:00"
    },
    {
      "@type": "OpeningHoursSpecification",
      "dayOfWeek": [
        "Saturday",
        "Sunday"
      ],
      "opens": "07:00",
      "closes": "23:00"
    }
  ]
}
</script>
```

### 3. Google Sitelinks Optimization Checklist
Sitelinks (seperti tampilan menu navigasi tambahan di hasil pencarian Google) dihasilkan secara otomatis oleh algoritma Google. Untuk memaksimalkan peluang mendapatkannya:
* **Struktur Navigasi Jelas**: Pastikan header menu menggunakan tag HTML semantik `<nav>` dengan link (`<a>`) yang memiliki teks deskriptif (misal: "Home", "Our Story", "Menu", "Gallery", "Location", "Contact").
* **Terapkan Sitemap XML**: Selalu daftarkan `sitemap.xml` di Google Search Console yang mendata seluruh rute penting.
* **Sitelinks Search Box Schema**: Gunakan skema `WebSite` dengan properti `potentialAction` untuk mengizinkan search box langsung di hasil Google.
* **SiteNavigationElement Schema**: Definisikan item menu utama menggunakan skema `SiteNavigationElement` agar Google mudah mengurai link-link penting.

```html
<!-- Sitelinks & Search Box Schema (JSON-LD) -->
<script type="application/ld+json">
[
  {
    "@context": "https://schema.org",
    "@type": "WebSite",
    "name": "deGudang",
    "url": "https://degudang.netlify.app",
    "potentialAction": {
      "@type": "SearchAction",
      "target": "https://degudang.netlify.app/?q={search_term_string}",
      "query-input": "required name=search_term_string"
    }
  },
  {
    "@context": "https://schema.org",
    "@type": "SiteNavigationElement",
    "@id": "#navigation-menu",
    "name": [
      "Home",
      "Our Story",
      "Menu",
      "Gallery",
      "Location",
      "Contact"
    ],
    "url": [
      "https://degudang.netlify.app/#hero",
      "https://degudang.netlify.app/#about",
      "https://degudang.netlify.app/#menu",
      "https://degudang.netlify.app/#instagram",
      "https://degudang.netlify.app/#footer",
      "https://degudang.netlify.app/#footer"
    ]
  }
]
</script>
```

### 4. AI-Scraper Optimization (`robots.txt`)
Ensure AI crawlers are explicitly allowed to index the public pages:
```txt
User-agent: Google-Extended
Allow: /

User-agent: GPTBot
Allow: /

User-agent: OAI-SearchBot
Allow: /
```
