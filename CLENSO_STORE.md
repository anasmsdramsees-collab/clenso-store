# Clenso Store — كلينزو

متجر إلكتروني لمنتجات شاي وقهوة وشوكولاتة فاخرة من شركة رمسيس للأغذية.

**Live Site:** https://anasmsdramsees-collab.github.io/clenso-store/
**GitHub Repo:** https://github.com/anasmsdramsees-collab/clenso-store

---

## Overview

Clenso is a single-page e-commerce store built in one HTML file. It sells premium tea, coffee, spices, and La Nova chocolates. The site is fully bilingual (Arabic / English) with RTL/LTR switching, a shopping cart, hero slideshow, and category filtering.

---

## Tech Stack

| Layer | Details |
|---|---|
| Structure | Single HTML file (`index.html`) |
| Styling | Inline CSS, CSS variables, responsive grid |
| Font | Cairo (Google Fonts) |
| Language | Vanilla JavaScript — no frameworks |
| Hosting | GitHub Pages |
| i18n | Custom JS translation system (`data-i18n` attributes) |

---

## File Structure

```
Clenso/
├── index.html              # Entire site — HTML, CSS, JS
├── logo/                   # Brand logos
│   ├── Asset 1.png         # Clenso logo
│   └── ChatGPT Image ...   # La Nova logo
├── posters/                # Hero slideshow images (JPEG, max 1400px)
│   ├── هيرو.jpg
│   ├── هيرو ٢.jpg
│   ├── بوستر العيد .jpg
│   ├── بوستر العيد ٢.jpg
│   ├── ظروف كرك.jpg
│   ├── IMG_8550.JPG
│   └── ChatGPT Image *.jpg  (16 AI-generated product posters)
└── products/
    ├── TEA/
    │   ├── كرك/
    │   │   ├── عبوة.png        # Karak tin
    │   │   └── ظروف كرك.png   # Karak sachets
    │   └── *.png              # Bahib Al Shay & Tea Bags (20 images)
    ├── COFFEE/
    │   ├── قهوة تركي/         # Turkish Coffee (4 products)
    │   ├── قهوة عربي /        # Arabic Coffee (1 product)
    │   ├── سبريسو/            # Espresso (6 products)
    │   ├── كبسولات قهوة/      # Capsules (13 images)
    │   └── قهورة سريعة/       # Instant Coffee (unused)
    ├── بهارات/                # Spices & Wellness (7 products)
    └──  chocolate/            # La Nova chocolate images (7 images)
```

---

## Product Categories

### Tea
| Category ID | Arabic | Products |
|---|---|---|
| `bahib` | بحب الشاي | 5 products — Bahib Al Shay blends |
| `teabags` | شاي أكياس | 11 products — assorted tea bags |
| `karak` | كرك | 2 products — Karak tin & sachets |

### Coffee
| Category ID | Arabic | Products |
|---|---|---|
| `turkish` | قهوة تركي | 4 products — Classic, Cardamom, Dark Roast, Original |
| `arabic` | قهوة عربية | 1 product — Arabic Coffee |
| `espresso` | سبريسو | 6 products — Premium Blend, Forte, Classico, Lungo, Decaf, Vanilla Latte |
| `capsules` | كبسولات | 8 products — Signature, Ristretto, Caramel, Hazelnut, Mocha, Almond, Coconut, Cinnamon |

### Spices & Wellness
| Category ID | Arabic | Products |
|---|---|---|
| `spices` | بهارات وصحة | 7 products — Matcha, Pomegranate, Saffron, Cinnamon, Turmeric, Ginger, Cardamom |

### La Nova Chocolates (separate section)
| ID | Product | Price |
|---|---|---|
| n1 | Dark Chocolate Bar | 55 SAR |
| n2 | Milk Chocolate Bar | 50 SAR |
| n3 | White Chocolate Bar | 50 SAR |
| n4 | Bonbons · 4 Pieces | 65 SAR |
| n5 | Bonbons · 8 Pieces | 115 SAR |
| n6 | Bonbons · 16 Pieces | 195 SAR |
| n7 | Bonbons · 24 Pieces (Eid Edition) | 275 SAR |
| n8 | Bonbons · 48 Pieces (Eid Grand Edition) | 495 SAR |

---

## Key Features

- **Bilingual** — Arabic (RTL) and English (LTR), toggle in navbar
- **Hero Slideshow** — 21 slides, auto-advance every 5s, only first image loads eagerly
- **Category Filter** — tabs filter products without page reload
- **Shopping Cart** — slide-in drawer, quantity controls, WhatsApp checkout (0539460440)
- **La Nova Section** — dedicated section for premium chocolate brand
- **Eid Edition Badges** — red gradient badge for Eid-exclusive products
- **Our Story Section** — brand story with hero image

---

## i18n System

Translations live in the `translations` object in `index.html`:

```js
const translations = {
  en: { cat_all: 'All Products', cat_bahib: 'Bahib Al Shay', ... },
  ar: { cat_all: 'كل المنتجات', cat_bahib: 'بحب الشاي', ... }
};
```

Elements with `data-i18n="key"` are updated automatically when language switches via `setLang(lang)`.

---

## JavaScript Architecture

| Function | Purpose |
|---|---|
| `renderProducts()` | Renders products for `currentCat` into `#productsGrid` |
| `renderNova()` | Renders La Nova chocolate products into `#novaGrid` |
| `switchCategory(cat)` | Updates `currentCat`, re-renders, scrolls to section |
| `initSlider()` | Builds hero slideshow from `posters[]` array |
| `addToCart(id)` | Adds product to cart, shows toast |
| `updateCartUI()` | Syncs cart drawer with current cart state |
| `setLang(lang)` | Switches site language, updates all `data-i18n` elements |

---

## Adding a New Product

1. Add image to the correct folder under `products/`
2. Add an entry to the `products` array in `index.html`:

```js
{
  id: 50,
  cat: 'turkish',         // category ID
  en: {
    name: 'Product Name',
    sub: 'Subtitle',
    desc: 'Description text.',
    tags: ['Tag1', 'Tag2']
  },
  ar: {
    name: 'اسم المنتج',
    sub: 'العنوان الفرعي',
    desc: 'وصف المنتج.',
    tags: ['وسم١', 'وسم٢']
  },
  price: 75,
  img: 'products/COFFEE/قهوة تركي/new_product.png'
}
```

---

## Adding a Hero Poster

1. Place image in `posters/` folder (JPEG preferred, max 1400px wide)
2. Add filename to the `posters` array in `index.html`:

```js
const posters = [
  'هيرو.jpg',
  'your_new_poster.jpg',  // ← add here
  ...
];
```

---

## Image Optimization

All images are optimized for web:

| Type | Max Dimension | Format | Approx Size |
|---|---|---|---|
| Product images | 800px | PNG | ~400–900 KB |
| Hero / posters | 1400px | JPEG 75% | ~250–450 KB |

To optimize a new image before adding:
```bash
# Resize product image to 800px
sips -Z 800 your_image.png

# Convert poster PNG to JPEG
sips -s format jpeg -s formatOptions 75 -Z 1400 poster.png --out poster.jpg
```

---

## Deployment

The site deploys automatically to GitHub Pages from the `main` branch.

```bash
# Push to go live
git add -A
git commit -m "Your message"
git push origin main
```

Live within ~2 minutes at: https://anasmsdramsees-collab.github.io/clenso-store/

---

## WhatsApp Checkout

Cart checkout sends an order summary via WhatsApp to **0539460440**.
The number is set in `index.html` in the `openWhatsApp()` function.

---

## Brand Info

- **Clenso** — tea, coffee & spices brand by Ramsees Foods (رمسيس للأغذية)
- **La Nova** — premium chocolate sub-brand
- **Products sourced from:** Ramsees Foudz (رمسيس فودز)
