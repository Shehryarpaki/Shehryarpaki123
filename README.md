# Strive Wearables — website

One page, `index.html`, published by GitHub Pages at **strivewearables.com**. No build step and no backend:
edit the file, push, and the site updates in about a minute.

`strive-arise-all-in-one.html` is an identical copy of `index.html`. After changing `index.html`, copy it over:
`cp index.html strive-arise-all-in-one.html`.

## What's on the page (top to bottom)

Hero → The Drift product card (photos, price, colours, Add to cart) → Strive Arise card (the last unit) → The Loop card
(out of stock) → Reviews → Inside the band → How it works → What it does → A day with Strive → Corporate gifting →
FAQ → closing call to action → footer (privacy notice).

**Products right now:** The Drift is the band on sale (PKR 15,000, Onyx, Glacier, Azure). The Loop is out of stock and shown as such.
One Strive Arise (Carbon, PKR 14,000) is left and can be added to the cart.

## Logo and icons

`favicon.ico`, `favicon-32.png`, `favicon-48.png`, `icon-192.png`, `icon-512.png` and `apple-touch-icon.png` use the
Instagram logo (white circle, blue-to-teal heartbeat with an arrow). Google shows `favicon-48.png` / `favicon.ico` next to
the site in search results and refreshes it on its own schedule.

## Product photos

All photos live in `img/`. Each colour of The Drift has two:

| Colour | Photos |
|---|---|
| Onyx (black) | `drift-onyx-studio.jpg` (studio view), `drift-onyx-sensor.jpg` (sensor close-up) |
| Glacier (whitish blue) | `drift-glacier-studio.jpg` (studio view), `drift-glacier-sensor.jpg` (sensor close-up) |
| Azure (blue) | `drift-azure-studio.jpg` (studio view), `drift-azure-sensor.jpg` (sensor close-up) |

- **Studio views** are still frames from the owner's own studio video of the three bands (dark background).
  The blue band in that video is navy, so in these stills (and in the Reel) it is colour-matched to the real Azure strap.
- **Sensor close-ups** come from one picture the supplier sent of the blue band (light background). The Azure one is that
  picture, turned to fit the portrait frame. Onyx and Glacier are the same picture with the strap and pod housing
  re-coloured; the black glass, sensor windows and metal buckle are untouched and the green status light is redrawn.
- The owner's phone photos of the whole band are no longer in the product gallery (removed at the owner's request).

Each photo is 900×1125 (portrait 4:5). Smaller copies are made from them so phones load less:

- `thumb-drift-<colour>-<view>.jpg` (160×200): the small buttons under the main photo, and the cart.
- `hero-drift-<colour>.jpg` (400×500): the three cards at the top of the page on phones, and the circles in the gifting section.
- `drift-inside.jpg`: the real sensor photo in "Inside the band".
- `og-drift.jpg` (1200×630): the preview shown when the link is shared on WhatsApp / Instagram / Facebook.
  WhatsApp and Facebook cache previews by file name, so a new preview image needs a **new file name**
  and the two `og:image` / `twitter:image` tags in `index.html` updated to match.
- `arise.jpg`, `thumb-arise.jpg`: the Strive Arise card and cart line.
- `social/`: the Instagram post images and the Reel (Instagram loads them from the site when a post is published).
- `loop-*`, `hero-carbon.jpg` etc.: The Loop's photos, kept for when it is back in stock.

The gallery lists which photos each colour has in `const GALLERY = {…}` in `index.html`. If a main photo is replaced,
its `thumb-` and `hero-` copies must be remade from it.

> Only **your own** product photos and video should go here. Don't use other brands' marketing images
> (for example photos of a similar-looking band from another company's store).

## Add to cart, cart and checkout (Shopify)

Every order goes through **Shopify checkout**. There is no WhatsApp order form.

- Pick a colour, set the quantity (starts at 1, max 10 per colour) and tap **Add to cart**. The cart slides in from the right.
- To mix colours, pick another colour and add it too. In the cart each colour is its own line with its own − / + and Remove.
- The **Strive Arise** card under the band has its own Add to cart (one unit, PKR 14,000). It goes into the same cart.
- **Checkout** in the cart opens Shopify checkout in the same tab with a line per item
  (so it works inside Instagram and WhatsApp's built-in browsers).
- **Buy it now** skips the cart and checks out just the colour and quantity shown.
- The cart icon in the header shows how many bands are in the cart, and the bottom bar on phones turns into "View cart (n)".
  The cart is kept until the browser tab is closed.

How checkout reaches Shopify (two ways, tried in this order):

1. The page asks Shopify for a cart (Storefront API, Buy Button channel) and opens its checkout link.
2. If that lookup is slow, fails or returns an error, the page opens a **Shopify cart link** instead:
   `https://strivewearables.myshopify.com/cart/<variant number>:<quantity>,…`, which also lands on Shopify checkout.
   The variant numbers are the `vid` values in `var ITEMS = {…}` in `index.html`
   (Shopify admin → Products → open the product → click a variant → the number at the end of the URL).
   **If a product or colour is recreated in Shopify, update its `vid`.**

Stock: when the lookup works, anything out of stock in Shopify shows as sold out and can't be added, and the last Arise
switches to "Sold out" by itself once it sells.

For it to work, in Shopify:

1. The band's product has **"Drift" in its title** and is **Active**. The Arise product has "Arise" in its title.
2. Both are published to the **Buy Button** channel (for way 1) and the **Online Store** channel (for way 2),
   and the online store is **not** password-protected (Online Store → Preferences).
3. The band has a **Colour** option with the values **Onyx**, **Glacier** and **Azure**, each with its own stock.

**Check it from your phone:** open `strivewearables.com/?shopify`. A box under the button lists what the site found
and which of the two ways checkout used.

Every other "Order now" button on the page (header, hero, bottom bar, closing section) jumps to this card.

**When The Loop is back:** restock it in Shopify, then ask for the site to be switched back (the Loop page is in git history).

## WhatsApp number

`const PHONE = "923210077442";` near the start of the last `<script>` block. International format, digits only
(for `0300 1234567` write `923001234567`). The same number is also written into the `https://wa.me/…` links in the
page, so search for `923210077442` and replace every one if it ever changes.

The review form and the corporate gifting form work the same way: they write a WhatsApp message with what the visitor typed, and the visitor presses send. Nothing is
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
| Someone adds a band to the cart | AddToCart | add_to_cart |
| Someone starts checkout | InitiateCheckout | begin_checkout |
| Someone taps "WhatsApp us" in the footer | Contact | contact |
| The gifting section scrolls into view | ViewContent | view_corporate_gifting |
| Someone sends a corporate quote request | Lead (`corporate_gifting`) | generate_lead (`lead_source: corporate_gifting`) |

In Google Analytics, mark `generate_lead` as a key event (Admin → Events) to count leads as conversions.

**Purchases happen on Shopify's checkout, not on this page**, so connect the same pixel inside Shopify too:
Shopify admin → Sales channels → **Facebook & Instagram** → Settings → Data sharing → choose this pixel.

## Rules for the copy

- Only claim what is true and confirmed. No invented reviews, press, awards, guarantees, delivery dates or discounts.
- Payment is by Bank Deposit only (no cash on delivery). Delivery is charged. Same-day delivery is Lahore only.
- IP68 is always written as "IP68 water-resistant" (only where it is confirmed for that band).
- Product names: "The Drift", "The Loop", "Strive Arise".
- Buttons say "Order now" (the product card itself uses "Add to cart" and "Buy it now"). The site no longer uses the word "pre-order".
- The Drift claims are limited to what is printed on its box or visible on the band: heart rate monitoring, sleep monitoring,
  100+ sports modes, no screen, woven strap with hook-and-loop fastening and a metal buckle, plus "works with iOS and
  Android" (confirmed by the owner). Battery life, water resistance, blood oxygen, call alerts and step counting are
  **not** stated until the owner confirms them.
- Never compare the band to, or name, another brand's product.
- A review goes on the page only if a real customer sent it.
