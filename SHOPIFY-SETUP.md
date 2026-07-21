# Strive Power on Shopify (Dawn) — pre-launch setup

Your business isn't released yet, so this sets up a **"coming soon" store**: the page
is live inside Dawn, but only people with the password can see it until you launch.

## A. Keep it private until launch (coming soon)
Shopify admin → **Online Store → Preferences** → scroll to **Password protection** →
tick **Restrict access to visitors with the password** → set a password → Save.
Now the public sees a coming-soon page; you can still preview everything.

## B. Add your product (as a draft for now)
1. **Products → Add product** → Title: `Strive Power`, price `14000`.
2. Upload your real photo(s).
3. Set status to **Draft** (or Active — it stays hidden while the store password is on).
4. Later you'll copy this product's **Variant ID** (see step E).

## C. Put the landing page in
1. **Settings → Files** → upload `band-black.png` → click **Copy link**.
2. Open `shopify-custom-liquid.html`, find `src="band-black.png"`, replace it with that link.
3. **Online Store → Themes → Customize**.
4. Pick the page (Home is fine) → **Add section → Custom Liquid**.
5. Paste the **entire** file into the box → **Save**.

Dawn's own header/footer are auto-hidden by the code, so it looks like the standalone site.
(If you want Dawn's menu/footer back, delete the first `<style>…</style>` block in the file.)

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
