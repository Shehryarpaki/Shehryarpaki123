# Strive Wearables — landing page

A single, dependency-free `index.html` for the Strive Wearables pre-order site
(screenless fitness band, Pakistan). No build step, no backend.

## 1. Set the WhatsApp number (required)

Open `index.html`, find this near the top of the `<script>` block:

```js
const PHONE = "923210077442"; // TODO: replace with the real number
```

Use the international format, **digits only — no `+`, no spaces**.
For a Pakistani number like `0300 1234567`, drop the leading `0` and prefix `92`:

```
0300 1234567  →  923001234567
```

The hero/footer/pre-order buttons and the WhatsApp handoff all use this one value.

## 2. Product photos

The product card shows **Strive The Loop** in three colourways and three views. All photos live in `img/`:

| | Angled view | Side view | Sensor view |
|---|---|---|---|
| Carbon (black) | `loop-carbon-angle.jpg` | `loop-carbon-side.jpg` | `loop-carbon-sensor.jpg` |
| Midnight (dark navy) | `loop-midnight-angle.jpg` | `loop-midnight-side.jpg` | `loop-midnight-sensor.jpg` |
| Cloud (white) | `loop-cloud-angle.jpg` | `loop-cloud-side.jpg` | `loop-cloud-sensor.jpg` |

`img/og-loop.jpg` (1200×630) is the image shown when the link is shared on WhatsApp / Instagram / Facebook.

To change a photo, replace the file and **keep the same file name**. Portrait 4:5 images around 900×1125 look best; keep each under ~150 KB so the page stays fast. Send new photos as the original files, not screenshots.

> Only **your own** product photos should go here. Don't use other brands' marketing images.

## Meta Pixel (Facebook / Instagram ads tracking)

The pixel code is already on the page but switched **off** until you add your Pixel ID. In `index.html`, find
`var META_PIXEL_ID = '';` and put the ID between the quotes (Meta Events Manager → Data sources → your pixel → the number under its name).

Events the site sends once it's on:

| Event | When |
|---|---|
| PageView | every visit |
| ViewContent | the product card scrolls into view (once per visit) |
| InitiateCheckout | someone taps Pre-order now (Shopify checkout or the WhatsApp form) |
| Lead | someone sends a pre-order on WhatsApp (value = order total in PKR) |
| Contact | someone taps "WhatsApp us" in the footer |

**Purchases happen on Shopify's checkout, not on this page**, so connect the same pixel inside Shopify too:
Shopify admin → Sales channels → **Facebook & Instagram** → Settings → Data sharing → choose this pixel. That sends Purchase events
(and Shopify's own server-side Conversions API) from checkout.

## 3. Link The Loop to Shopify checkout

The "Pre-order now" button in the product card is the same Shopify Buy Button the Arise used. It finds your product automatically and opens Shopify checkout in the same tab (so it works inside Instagram and WhatsApp's built-in browsers). For it to appear:

1. The product has **"Loop" in its title** (e.g. "Strive The Loop") and is **Active**.
2. It is published to the **Buy Button** sales channel (product page → *Publishing* / *Sales channels* → tick **Buy Button**). The site's Shopify key only sees products on that channel.
3. It can be sold: either it has stock, or each variant has **"Continue selling when out of stock"** ticked — that's how Shopify takes pre-orders.

**Check it from your phone:** open `strivewearables.com/?shopify` — a box under the button lists the products the site can see and says exactly why it's using Shopify or WhatsApp.

If anything is missing, customers still get a working "Pre-order now" button that sends the order on WhatsApp.

To pin a specific product instead, open `index.html`, find `var LOOP_SHOPIFY_PRODUCT_ID = '';` and paste the product's ID between the quotes (Shopify admin → Products → open the product → the number at the end of the URL).

## 4. Get an email for every order (Netlify Forms)

The site sends each pre-order to **Netlify Forms**, so you get an email + a list of
orders in your Netlify dashboard. To switch the emails on (one time):

1. Deploy the site on Netlify (see below).
2. In Netlify → your site → **Forms** — you'll see a form called **`preorder`**.
3. Click **Form notifications → Add notification → Email notification**, enter your
   email, save.

Now every submitted pre-order emails you (name, WhatsApp, city, model, colour,
quantity, payment) **and** still opens WhatsApp for the customer. Orders are also
listed under **Forms → preorder** in the dashboard.

> Not on Netlify? You can instead use Formspree: set `FORMSPREE_ENDPOINT` near the
> top of the script to your Formspree URL and it will email you too.

## 4. Editing after you publish

- **If you deployed by dragging the file to Netlify Drop:** edit `index.html`, then
  drag the folder onto Netlify again — it updates the same site.
- **If you connected Netlify to GitHub (recommended):** just change the file in
  GitHub (or ask me to) — Netlify redeploys automatically in ~30 seconds.
- **Shopify:** edit anytime in the Shopify editor; changes save live.

## 5. Other placeholders to replace

- **Instagram handle** — in the footer, currently `https://instagram.com/strivewearables`.
- **OG image** — `img/og-loop.jpg`; replace the file to change the social preview.

## 4. Optional: also save orders to Formspree (disabled by default)

Orders go straight to WhatsApp. If you also want a copy saved server-side,
create a free [Formspree](https://formspree.io) form and set:

```js
const FORMSPREE_ENDPOINT = "https://formspree.io/f/xxxxxxxx";
```

Leave it as `""` to keep it off. It's fire-and-forget and never blocks the WhatsApp step.

## 5. Deploy (Netlify Drop)

1. Go to <https://app.netlify.com/drop>.
2. Drag the folder containing `index.html` (or just the file) onto the page.
3. Netlify will ask you to create a **free account** (click "Continue with GitHub/Google" to skip making a password). This is required to host the site.
4. You get a live URL instantly. Optionally connect a custom domain in Site settings.

That's it — no other steps needed.
