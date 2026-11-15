# Maulie Cosmetics — SEO Implementation Report
**Site:** https://www.mauliecosmetics.com/ · **Date:** 13 Nov 2026 · **Scope:** single-page site (`index.html`) + new support files

---

## 1. Files in this package — upload ALL to the website root (same folder as index.html)

| File | Purpose |
|---|---|
| `index.html` | Optimised homepage (replaces the old file) |
| `404.html` | Branded "page not found" page (noindex) |
| `robots.txt` | Crawl rules + sitemap location |
| `sitemap.xml` | XML sitemap for Google / Bing |
| `.htaccess` | HTTPS + www redirect, 404, compression, caching (Apache/cPanel/Hostinger only) |
| `site.webmanifest` | Mobile / PWA icon manifest |
| `llms.txt` | Plain factual company summary for AI search tools |
| `maulie-cosmetics-logo-200/420/840.webp` | Logo (replaces 3 × 270 KB embedded base64 copies) |
| `maulie-cosmetics-logo.png` | Logo for Google (Organization schema) |
| `og-image.jpg` | 1200×630 share image for WhatsApp, LinkedIn, Facebook, X |
| `favicon.ico`, `favicon-32x32.png`, `apple-touch-icon.png`, `icon-192.png`, `icon-512.png` | Browser / phone icons |

**Keep on the server:** the existing `maulie-hero-3d-left/right-800/1200.webp/.avif` files — the hero still uses them.

---

## 2. Title & meta description

| Page | Title (≤60) | Meta description (≤155) |
|---|---|---|
| Home `/` | Cosmetics Manufacturer in Mumbai & India \| Maulie Cosmetics | Maulie Cosmetics: private label & third party cosmetics manufacturer in Navi Mumbai for skincare, haircare & personal care brands across India. |
| 404 | Page Not Found \| Maulie Cosmetics | (noindex) |

Open Graph / Twitter title: *Maulie Cosmetics | Private Label & Third Party Cosmetics Manufacturer in India*

---

## 3. Keyword mapping (single page → by section)

| Section (anchor) | Heading | Target keywords |
|---|---|---|
| `<title>`, meta, H1 (hero) | Luxury Cosmetics & Personal Care Manufacturer in India | cosmetics manufacturer in India, cosmetics manufacturer in Mumbai, premium cosmetics manufacturer, personal care products manufacturer |
| About `#about` | Premium Cosmetic Manufacturer in Mumbai & Navi Mumbai | cosmetics manufacturer in Navi Mumbai / Mumbai, cosmetic manufacturing company, private label cosmetics manufacturer, third party cosmetics manufacturer |
| Services `#services` (H2) | Private Label & Third Party Cosmetics Manufacturer in India | private label / third party cosmetics manufacturer in India |
| `#private-label` | Private Label Cosmetics Manufacturing | private label cosmetics manufacturer, white label cosmetics, start your own cosmetics brand, bulk cosmetics manufacturing |
| `#third-party` | Third Party & Contract Manufacturing | third party cosmetics manufacturer, cosmetic contract manufacturing, cosmetic OEM / ODM manufacturer India |
| `#skincare-manufacturing` | Skincare Manufacturing Solutions | skincare (products) manufacturer, face wash / face cream / face serum / sunscreen / body lotion manufacturer, vitamin C & niacinamide serum (on request) |
| `#haircare-manufacturing` | Haircare Manufacturing Solutions | hair care products manufacturer, shampoo / hair oil manufacturer, herbal / sulphate-free / anti-dandruff shampoo, conditioner, hair serum (on request) |
| `#personal-care-manufacturing` | Personal Care, Bath & Body | personal care products manufacturer, body wash manufacturer, bath and body products manufacturer |
| `#home-care` | Home & Hygiene Care Products | home care products manufacturer, household cleaning products manufacturer (toilet cleaner, hand wash) |
| Products `#products` | Skincare & Haircare Products Manufacturer | product-level terms (14 categories) |
| Hotel kits `#hotel-kits` | Custom Hotel Amenity Kit Manufacturer | hotel amenity kit manufacturer India |
| Facility `#manufacturing` | Manufacturing Facility — Bathija Industries, Kamothe | cosmetic factory Navi Mumbai |
| Process `#process` | Our Cosmetic Manufacturing Process | cosmetic manufacturing process, custom cosmetic formulation |
| `#quality-assurance` | Quality Built Into Every Batch | quality assurance, GMP-compliant |
| `#start-your-brand` | Start Your Own Cosmetics Brand | start your own cosmetics brand, cosmetics manufacturing for startups |
| FAQ `#faq` (11 Q&A) | Cosmetic Manufacturing FAQs | long-tail questions (private label vs third party, MOQ, startups, locations) |
| Locations `#locations` | Cosmetics Manufacturer for Mumbai, Navi Mumbai, Thane & Pune | cosmetics manufacturer in Mumbai / Navi Mumbai / Panvel / Thane / Pune / Maharashtra |

"…Near Me" keywords are not written into the page (that reads unnaturally). Google ranks "near me" searches mainly on your **Google Business Profile** + address consistency — see section 6.

---

## 4. What was implemented

### Critical fixes
1. **Hidden H1 removed** — the old `<h1 style="display:none">` is gone. The hero headline is now a real, visible H1.
2. **Hidden keyword text removed** — the near-invisible footer "SEO keyword cloud" is a Google spam signal and has been deleted.
3. **Page weight cut by ~70%** — the logo was embedded 3 times as base64 (≈810 KB). It now loads as small WebP files. HTML: 1.11 MB → 0.33 MB (≈80 KB gzipped).
4. **Broken Google Maps fixed** — both map iframes used invalid `pb=` embed codes. They now use working address-based embeds.

### Technical SEO
- New title, meta description, canonical (HTTPS + www), `lang="en-IN"`, theme-color
- Open Graph + Twitter Card with a real 1200×630 image (was missing)
- Removed `meta keywords` (ignored by Google, a spam signal on Bing) and the wrong `geo.position` (pointed to South Mumbai)
- Clean heading structure: 1 × H1 → H2 per section → H3 (facility cards changed H4→H3; footer titles H4→H2)
- Removed conflicting/incomplete microdata (`itemscope` on `<html>` and location cards) — JSON-LD is now the single source of truth
- Internal linking: new nav items (Services, FAQ); footer Services column links to each service anchor
- Favicon set, web manifest, `robots.txt`, `sitemap.xml`, `404.html`, `.htaccess`
- Accessibility: removed incorrect `role="menubar"` from the nav; `width`/`height` on all logos (prevents layout shift)

### Structured data (JSON-LD `@graph`)
`Organization` (logo, legal name, GST, contact point, both addresses, service catalogue) · `LocalBusiness` (factory address, hours, areas served) · `WebSite` · `WebPage` · `FAQPage` (generated from the 11 visible FAQs — exact match).
**Not added (on purpose):** `Product` (no individual product pages/prices), `Review`/`AggregateRating` (needs verified reviews), `BreadcrumbList` (single page — no hierarchy), `Article` (no blog).
Note: Google now shows FAQ rich results mainly for government/health sites; the FAQ markup still helps AI search and Bing.

### Performance (Core Web Vitals)
- LCP: hero logo is preloaded with `fetchpriority="high"` and responsive `srcset` (420/840 px)
- EmailJS script now `defer` (no longer blocks rendering) — initialised on first use, forms work as before
- Removed unused **Poppins** font family from the Google Fonts request
- Fixed `preconnect` to images.unsplash.com (crossorigin flag was opening the wrong connection)
- `.htaccess`: gzip + 1-year image caching

### New content (≈1,000 words, all based on your existing offering)
- **Manufacturing Services** — 6 cards: Private Label · Third Party/Contract · Skincare · Haircare · Personal Care/Bath & Body · Home & Hygiene
- **Manufacturing Process** — 6 steps
- **Quality Assurance** panel + **Start Your Own Cosmetics Brand** panel
- **At-a-glance facts box** in About (helps Google AI Overviews / ChatGPT / Perplexity quote you correctly)
- **Service-area block** (Mumbai, Navi Mumbai, Panvel, Thane, Pune, PAN India) — one honest block, no copied city doorway pages
- **6 new FAQs** (11 total)

### Conversion tracking (ready, no IDs inserted)
Every WhatsApp, call and email click pushes an event (`whatsapp_click`, `phone_click`, `email_click`) to `dataLayer` / GA4. Successful form or chatbot inquiries fire `generate_lead`. These start working as soon as GTM or GA4 is installed.

### Preserved unchanged
Design (navy-gold palette from the logo), logo animations, hero 3D images, product grid, hotel kits, vision & mission, facility gallery + lightbox, video, testimonials, contact form + EmailJS, AI chatbot, WhatsApp float button.

---

## 5. ⚠️ Please verify before going live (honesty / legal)

| Item | Where | Why it matters |
|---|---|---|
| **Testimonials** (Rahul Mehta, Priya Shah, Arjun Verma, Sunita Joshi) | `#testimonials` | If these are not real clients, remove or replace them. Fake reviews break Google's policies and India's consumer-protection rules on online reviews. No review schema was added. |
| **"ISO" stat** in the stats strip | below hero | Keep only if you hold an ISO certificate — otherwise change it (e.g. "GMP" or "R&D"). |
| **GMP wording** | About, Features, QA panel | Now consistently "GMP-compliant". If you hold a GMP *certificate* (e.g. FDA Maharashtra), say so and name it. |
| **On-request products** | Skincare & Haircare cards | Vitamin C / niacinamide serums, conditioner, hair serum, herbal / sulphate-free / anti-dandruff shampoo are worded "developed on request". Confirm you can make them; remove any you can't. |
| **Stock photos** | products, facility | Already labelled "illustrative". Replacing them with real factory/product photos (named like `maulie-cosmetics-factory-kamothe.webp`) is the single biggest trust + image-SEO upgrade. |

---

## 6. Manual configuration still needed

1. **Upload all files** in this package to the site root; keep the hero 3D images.
2. **Google Search Console** — verify + submit sitemap (steps in section 7).
3. **Bing Webmaster Tools** — sign in at bing.com/webmasters → "Import from Google Search Console" (fastest) → submit `sitemap.xml`.
4. **Analytics** — create GA4 (and optionally GTM). In `index.html` `<head>`, uncomment ONE block (GTM *or* GA4) and replace `GTM-XXXXXXX` / `G-XXXXXXXXXX`. In GA4 → Admin → Events, mark `generate_lead` and `whatsapp_click` as **Key events**.
5. **Google Business Profile** (most important for "near me" searches) — claim/verify the Kamothe factory; category "Cosmetics manufacturer" (secondary: "Manufacturer", "Personal care products manufacturer"); add website, hours Mon–Sat 9:30–18:00, real photos; keep name/address/phone exactly as on the website.
6. **Exact map coordinates** — once GBP is verified, copy the latitude/longitude and add a `"geo"` block to the LocalBusiness schema (removed because the old coordinates were inaccurate).
7. **Social profiles** — when you have LinkedIn / Instagram / Facebook / IndiaMART pages, add their URLs as a `"sameAs": [...]` list in the Organization schema.
8. **Hosting not Apache?** Netlify / Vercel / Cloudflare ignore `.htaccess` — set the HTTPS + www redirect and 404 page in their dashboard instead.
9. **HTTPS** — confirm the SSL certificate is active and `http://mauliecosmetics.com` redirects to `https://www.mauliecosmetics.com/`.

---

## 7. Google Search Console — submission steps

1. Go to **search.google.com/search-console** → *Add property* → choose **Domain** → enter `mauliecosmetics.com`.
2. Copy the **TXT record** → add it in your domain DNS (GoDaddy / Hostinger / BigRock) → click **Verify** (may take up to a few hours).
   *Alternative:* choose *URL prefix* → `https://www.mauliecosmetics.com/` → *HTML tag* → paste the code into the commented `google-site-verification` line in `index.html` and uncomment it.
3. Left menu → **Sitemaps** → enter `sitemap.xml` → **Submit**. Status should show "Success".
4. Top bar → **URL Inspection** → paste `https://www.mauliecosmetics.com/` → **Request indexing**.
5. After 3–7 days check **Pages** (indexing), **Core Web Vitals**, **Enhancements** (FAQ / structured data) for errors.
6. Validate schema anytime at **search.google.com/test/rich-results** and **validator.schema.org**.

---

## 8. Final SEO audit checklist

| ✓ | Check | Status |
|---|---|---|
| ✅ | Unique title & meta description | Done |
| ✅ | Canonical HTTPS + www | Done |
| ✅ | Exactly one visible H1, logical H2/H3 order | Done |
| ✅ | No hidden text / keyword stuffing | Done (removed) |
| ✅ | All 28 images have alt text | Done |
| ✅ | Logos with width/height (no layout shift) | Done |
| ✅ | Open Graph + Twitter Card + share image | Done |
| ✅ | JSON-LD valid (Organization, LocalBusiness, WebSite, WebPage, FAQPage) | Done — parsed & checked |
| ✅ | FAQ schema matches visible FAQ | Done (11/11) |
| ✅ | No broken internal anchors | Done — all checked |
| ✅ | Google Maps embeds working | Fixed |
| ✅ | robots.txt, sitemap.xml, 404.html, favicon, manifest | Done |
| ✅ | Render-blocking script removed, unused font removed | Done |
| ✅ | Mobile layout of new sections (390 px) | Tested |
| ✅ | No JavaScript errors; FAQ, nav, form logic intact | Tested |
| ⬜ | Search Console verified + sitemap submitted | You |
| ⬜ | GA4 / GTM ID added, key events marked | You |
| ⬜ | Google Business Profile verified | You |
| ⬜ | Testimonials / ISO / on-request products confirmed | You |
| ⬜ | Real factory & product photos | You |
| ⬜ | PageSpeed Insights test after upload (pagespeed.web.dev) | You |

---

## 9. Recommended next step (biggest ranking gain)

A one-page site can rank for the brand and a few core terms, but separate pages win the competitive ones. Next phase: dedicated pages with unique content for **/private-label-cosmetics-manufacturer/**, **/third-party-cosmetics-manufacturer/**, **/skincare-manufacturer/**, **/haircare-manufacturer/** and **/hotel-amenity-kits/**, plus a small blog (e.g. "How to start a cosmetics brand in India", "Private label vs third party manufacturing") with Article and BreadcrumbList schema.
