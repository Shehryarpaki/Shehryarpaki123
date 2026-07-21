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

## 2. Product photo

The product section uses one **image file** that ships with the site: `band-black.png`.

To use your **own** photo, just replace that file — **keep the same file name** (`band-black.png`) and it works instantly (a square ~1000×1000 image on a dark background looks best). No HTML edits needed.

> Note: only **your own** product photos should go here. Don't use other brands' marketing images.

## 3. Get an email for every order (Netlify Forms)

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

- **Instagram handle** — in the footer: `https://instagram.com/your_handle_here`.
- **OG image** — the `og:image` meta points to a placeholder URL; host a 1200×630 image and update it for nice social previews.

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
