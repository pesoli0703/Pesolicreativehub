# Pesoli Creative Hub

A black-and-gold portfolio website for photo restoration, portrait design, creative editing, and retouching.

## Latest portfolio

The website showcases 11 supplied works: the five photographs from the previous update plus six new additions. Each has responsive AVIF/WebP display images and a locally stored full-size WebP for the viewer. The uploads have not been retouched or generatively edited for the website.

### New additions

These six works are featured in the hero slideshow and appear first in the gallery.

| Work | Collection | Full-size asset |
| --- | --- | --- |
| Red print portrait | Portraits | `assets/portfolio/red-print-portrait.webp` |
| Gold accents portrait | Portraits | `assets/portfolio/gold-accents-portrait.webp` |
| Black dress by the mirror | Portraits | `assets/portfolio/black-dress-mirror.webp` |
| 90th birthday in blue | Celebrations | `assets/portfolio/ninetieth-birthday-blue.webp` |
| Retirement & 60th birthday | Celebrations | `assets/portfolio/retirement-sixtieth-birthday.webp` |
| 90th birthday in green | Celebrations | `assets/portfolio/ninetieth-birthday-green.webp` |

### Previously added photographs

All five remain available in the gallery and full-size viewer.

| Photograph | Collection | Full-size asset |
| --- | --- | --- |
| Pastel tones on the stairs | Portraits | `assets/portfolio/pastel-stairway.webp` |
| Courtyard in blue | Outdoor | `assets/portfolio/courtyard-portrait.webp` |
| Pastel portrait by the staircase | Portraits | `assets/portfolio/pastel-portrait.webp` |
| Gold mirror portrait | Portraits | `assets/portfolio/gold-mirror-portrait.webp` |
| Poolside in blue | Outdoor | `assets/portfolio/blue-poolside.webp` |

Gallery filters show all 11 works, six portraits, two outdoor photographs, or three celebration designs. The hero features the six newest uploads. Images fit within their frames without cropping, preserving the tall portraits and the retirement design's lettering.

## Content cleanup

- Removed the previous remote demo images and obsolete image-host links.
- Removed sample client reviews and unverified customer, photo-count, and satisfaction statistics.
- Removed the old before/after demonstration: no matching originals were supplied for the new photographs. The restoration service and its enquiry link remain available.
- Removed the loading screen that could obscure the page while waiting for external resources.
- Replaced unsupported response-time and turnaround promises with an invitation to confirm project details on WhatsApp.
- Kept the existing business name, services, WhatsApp number, and Instagram link.

## Features

- Responsive navigation and a keyboard-accessible mobile menu.
- Six-photo hero slideshow featuring the newest uploads with manual selection, pause/play, and reduced-motion support.
- Static HTML portfolio: photographs and full-size links remain available without JavaScript.
- Accessible native-dialog image viewer with previous/next controls, arrow keys, Escape to close, and focus restoration.
- Portrait, outdoor, and celebration filters with a live result count.
- Keyboard-accessible FAQ buttons.
- Direct WhatsApp enquiry links, including a pre-filled message.
- Locally hosted images and fonts; no third-party scripts or image hosts are required to render the site.
- Responsive AVIF sources with WebP fallbacks, lazy-loaded gallery images, and explicit image dimensions.
- Only the first hero image is loaded initially on mobile. Other slides load on selection or shortly before automatic playback; automatic downloads pause offscreen, in hidden tabs, with reduced motion, or with Data Saver enabled.
- The full-size viewer downloads its selected photograph on demand and waits for it to decode before prefetching the next one.
- Scroll-progress and pointer-glow updates are batched with `requestAnimationFrame`.

## Loading performance

Display images are generated at 320, 540, and 880 pixels wide in both AVIF and WebP. The browser chooses the appropriate size for the viewport and pixel density. Original full-size viewer images are unchanged.

Controlled local Chromium measurements before and after this update:

| Median of three cold-cache mobile runs | Before | After |
| --- | ---: | ---: |
| Load event | 10.81 s | 1.13 s |
| Largest Contentful Paint | 7.70 s | 1.86 s |
| Initial encoded transfer | 2.10 MB | 167 KB |
| Initial requests | 14 | 8 |

Test profile: 390 × 844 viewport at 2× pixel density, 1.6 Mbps download, 750 kbps upload, 150 ms latency, 4× CPU throttling, and Brotli-compressed HTML. Network totals were captured at the load event; LCP was sampled after image decoding and a short settling period. These are local comparisons, not production Lighthouse scores or a guarantee for every visitor/network.

`vercel.json` adds long-lived immutable caching for versioned display images and local fonts, shorter caching with stale-while-revalidate for full-size portfolio images, and revalidation for the HTML document. When replacing a display image or font, use a new filename/version path rather than overwriting an immutably cached file.

## Project structure

```text
Pesolicreativehub/
├── index.html                 # Page markup, styles, and interactions
├── vercel.json                # Static-asset caching and response headers
├── assets/
│   ├── LUCIDE-LICENSE.txt      # License for the vector icons
│   ├── optimized/v1/          # Responsive AVIF/WebP hero and gallery images
│   ├── portfolio/             # Eleven full-size WebPs and legacy thumbnails
│   └── fonts/                 # Poppins, Playfair Display, and their licenses
└── README.md
```

This is a static website. There are no packages to install and no build step.

## Preview locally

From the repository root:

```sh
python -m http.server 3000 --bind 0.0.0.0
```

Open `http://localhost:3000` when browsing on the same computer. In a hosted development preview, use the preview URL supplied by the platform. Keep the `assets` directory beside `index.html` so the relative image and font links resolve correctly.

## Update the portfolio

1. Add the full-size WebP to `assets/portfolio/` and generate 320/540/880-pixel AVIF and WebP derivatives under a new version path in `assets/optimized/`. Preserve aspect ratios and include appropriate alternative text.
2. Update the first `picture.hero-slide`, the `heroSlideData` JSON metadata, and the slideshow selection buttons in `index.html`. Keep deferred slides free of active `src`/`srcset` attributes until selection.
3. Add matching gallery links in `galleryContainer`, including the full-size `href`, responsive `picture` sources, lazy-loaded fallback `img`, title, alternative text, dimensions, and `data-category` (`portraits`, `outdoor`, or `celebrations`).
4. Update the filter counts, initial gallery status, and initial image counters to match the new collection.
5. If the first featured photo changes, update its responsive preload and social-preview image references in the document head. Keep preload sizes/srcsets aligned with the first hero picture.
6. Check the gallery, filters, full-size viewer, all slideshow controls, automatic playback/pause, WebP fallback, reduced motion, mobile layouts, and initial network requests before publishing.

Only publish client photographs with permission. Add reviews, statistics, or before/after comparisons only when authentic content is available. For a comparison, use a matching original and edited result rather than unrelated photographs.

## Publish

Upload `index.html`, `vercel.json`, and the complete `assets/` directory to the static host. The existing website is hosted on Vercel at `pesolicreativehub.vercel.app`; publish the reviewed commit to that project's production environment. Keep the cache headers when deploying through Vercel. Other hosting providers need equivalent cache rules.

The social-preview URL and image point to the existing `pesolicreativehub.vercel.app` site. Update them if the website moves to a different domain.

## Contact

- WhatsApp: +234 810 961 5982
- Instagram: `@pesolicreativehub`

## Font licenses

Poppins and Playfair Display are distributed under the SIL Open Font License. Their license files are included in `assets/fonts/`. The Lucide vector icons are covered by the license in `assets/LUCIDE-LICENSE.txt`.

Updated November 8, 2026: 11 works, responsive image delivery, deferred loading, and static-asset caching.
