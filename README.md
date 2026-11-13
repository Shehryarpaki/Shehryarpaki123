# Strive Wearables — website

One page, `index.html`, published by GitHub Pages at **strivewearables.com**. No build step and no backend:
edit the file, push, and the site updates in about a minute.

`strive-arise-all-in-one.html` is an identical copy of `index.html`. After changing `index.html`, copy it over:
`cp index.html strive-arise-all-in-one.html`.

## What's on the page (top to bottom)

Hero → The Loop product card (photos, price, colours, buy button) → Reviews → Inside the band → How it works →
What it tracks → A day with Strive → Corporate gifting → FAQ → closing call to action → footer (privacy notice).

## Product photos

All photos live in `img/`. The Loop has three colourways and three views:

| | Angled view | Side view | Sensor view |
|---|---|---|---|
| Carbon (black) | `loop-carbon-angle.jpg` | `loop-carbon-side.jpg` | `loop-carbon-sensor.jpg` |
| Midnight (dark navy) | `loop-midnight-angle.jpg` | `loop-midnight-side.jpg` | `loop-midnight-sensor.jpg` |
| Cloud (white) | `loop-cloud-angle.jpg` | `loop-cloud-side.jpg` | `loop-cloud-sensor.jpg` |

Each photo is 900×1125 (portrait 4:5). Smaller copies are made from them so phones load less:

- `thumb-<colour>-<view>.jpg` (160×200): the small buttons under the main photo.
- `hero-<colour>.jpg` (400×500): the three cards at the top of the page on phones, and the circles in the gifting section.
- `og-loop-2.jpg` (1200×630): the preview shown when the link is shared on WhatsApp / Instagram / Facebook.
  WhatsApp and Facebook cache previews by file name, so a new preview image needs a **new file name**
  (`og-loop-3.jpg`, …) and the two `og:image` / `twitter:image` tags in `index.html` updated to match.

If a main photo is replaced, its `thumb-` and `hero-` copies must be remade from it.

> Only **your own** product photos should go here. Don't use other brands' marketing images.

## Buy button (Shopify)

"Order now" in the product card is a Shopify Buy Button. It finds the product automatically and opens Shopify
checkout in the same tab (so it works inside Instagram and WhatsApp's built-in browsers). For it to appear:

1. The product has **"Loop" in its title** and is **Active**.
2. It is published to the **Buy Button** sales channel (product page → *Publishing* / *Sales channels* → tick **Buy Button**).
   The site's Shopify key only sees products on that channel.
3. It can be sold: either it has stock, or each variant has **"Continue selling when out of stock"** ticked
   (that's how Shopify takes pre-orders).

**Check it from your phone:** open `strivewearables.com/?shopify`. A box under the button lists the products the
site can see and says exactly why it is using Shopify or WhatsApp.

If Shopify can't be reached, customers still get a working "Order now" button that sends the order on WhatsApp.

To pin a specific product, find `var LOOP_SHOPIFY_PRODUCT_ID = '';` in `index.html` and paste the product's ID between
the quotes (Shopify admin → Products → open the product → the number at the end of the URL).

Every other "Order now" button on the page (header, hero, bottom bar, closing section) jumps to this buy button.

## WhatsApp number

`const PHONE = "923210077442";` near the start of the last `<script>` block. International format, digits only
(for `0300 1234567` write `923001234567`). The same number is also written into the `https://wa.me/…` links in the
page, so search for `923210077442` and replace every one if it ever changes.

The order form (shown only when Shopify can't load), the review form and the corporate gifting form all work
the same way: they write a WhatsApp message with what the visitor typed, and the visitor presses send. Nothing is
stored on the site.

## Corporate gifting

The section at `strivewearables.com/#gifting` (share that link with companies). The form asks for company, quantity
and city, with optional colours, date, invoice and notes, and opens WhatsApp with a quote request.

What it states, all confirmed by the owner: bulk pricing on larger orders, company invoice
provided, custom branding and gift packaging possible on larger orders, delivery across Pakistan. It shows no price, no discount
figure, no minimum order and no delivery date (the owner quotes each order). Add those only when they are decided.

## Tracking

**Google Analytics** (`G-XPQBX4V1DW`) is on. **Meta Pixel** is on the page but switched **off** until a Pixel ID is
added: find `var META_PIXEL_ID = '';` in `index.html` and put the ID between the quotes
(Meta Events Manager → Data sources → your pixel → the number under its name).

| What happens | Meta Pixel event | Google Analytics event |
|---|---|---|
| Any visit | PageView | page_view |
| The product photo scrolls into view | ViewContent | view_item |
| Someone starts checkout (Shopify or the WhatsApp form) | InitiateCheckout | begin_checkout |
| Someone sends an order on WhatsApp | Lead (value = band total) | generate_lead |
| Someone taps "WhatsApp us" in the footer | Contact | contact |
| The gifting section scrolls into view | ViewContent | view_corporate_gifting |
| Someone sends a corporate quote request | Lead (`corporate_gifting`) | generate_lead (`lead_source: corporate_gifting`) |

In Google Analytics, mark `generate_lead` as a key event (Admin → Events) to count leads as conversions.

**Purchases happen on Shopify's checkout, not on this page**, so connect the same pixel inside Shopify too:
Shopify admin → Sales channels → **Facebook & Instagram** → Settings → Data sharing → choose this pixel.

## Rules for the copy

- Only claim what is true and confirmed. No invented reviews, press, awards, guarantees, delivery dates or discounts.
- Payment is by Bank Deposit only (no cash on delivery). Delivery is charged. Same-day delivery is Lahore only.
- IP68 is always written as "IP68 water-resistant".
- The product is "The Loop" (never "Strive The Loop" in visible text).
- Buttons say "Order now". The site no longer uses the word "pre-order".
- A review goes on the page only if a real customer sent it.
