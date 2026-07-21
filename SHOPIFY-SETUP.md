# Strive Arise on Shopify (Dawn) — pre-launch setup

Your business isn't released yet, so this sets up a **"coming soon" store**: the page
is live inside Dawn, but only people with the password can see it until you launch.

## A. Keep it private until launch (coming soon)
Shopify admin → **Online Store → Preferences** → scroll to **Password protection** →
tick **Restrict access to visitors with the password** → set a password → Save.
Now the public sees a coming-soon page; you can still preview everything.

## B. Add your product (as a draft for now)
1. **Products → Add product** → Title: `Strive Arise`, price `14000`.
2. Upload your real photo(s).
3. Set status to **Draft** (or Active — it stays hidden while the store password is on).
4. Later you'll copy this product's **Variant ID** (see step E).

## C. Put the landing page in (two paste blocks)

Shopify limits each Custom Liquid section to 50 KB, so the page comes in **two files** —
`shopify-paste-1.html` and `shopify-paste-2.html`. You add **two** Custom Liquid sections,
one after the other.

1. **Settings → Files** → upload `band-black.png` → click **Copy link**.
2. Open `shopify-paste-1.html`, find `src="band-black.png"`, replace it with that link.
3. **Online Store → Themes → Customize** → pick the page (Home is fine).
4. **Add section → Custom Liquid** → paste **all of `shopify-paste-1.html`** → Save.
5. **Add section → Custom Liquid** *again, directly below the first* → paste **all of
   `shopify-paste-2.html`** → Save.

Order matters: PASTE 1 must be above PASTE 2. Together they render as one page, and
Dawn's own header/footer are auto-hidden so it looks like the standalone site.
(To bring Dawn's menu/footer back, delete the first `<style>…</style>` block in PASTE 1.)

## D. Orders right now (before launch)
The **Pre-order** button opens the form and sends the order to your **WhatsApp**
(`0321 0077442`). This works immediately — good for taking pre-orders while unreleased.

## E. Launch day — switch to real Shopify checkout (optional)
When you're ready to sell through Shopify (real cart, payment, orders in your dashboard):
1. Open the product → on the variant, copy the **Variant ID**
   (it's the long number in the URL: `.../variants/**1234567890**`).
2. In `shopify-custom-liquid.html`, find `const SHOPIFY_VARIANT_ID = "";`
   and put the number inside the quotes: `const SHOPIFY_VARIANT_ID = "1234567890";`
3. Save the section. Now **Pre-order** sends customers to Shopify checkout instead of WhatsApp.
4. Turn OFF the store password (Preferences) to go live.

## Payments in Pakistan (for step E)
Shopify's own card processor isn't available in Pakistan. Use **Cash on Delivery**
(Settings → Payments → Manual methods) and/or a third-party gateway app (e.g. PayFast)
from the Shopify App Store.
