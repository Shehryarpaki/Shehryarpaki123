# Strive Wearables — landing page

A single, dependency-free `index.html` for the Strive Wearables pre-order site
(screenless fitness band, Pakistan). No build step, no backend.

## 1. Set the WhatsApp number (required)

Open `index.html`, find this near the top of the `<script>` block:

```js
const PHONE = "923000000000"; // TODO: replace with the real number
```

Use the international format, **digits only — no `+`, no spaces**.
For a Pakistani number like `0300 1234567`, drop the leading `0` and prefix `92`:

```
0300 1234567  →  923001234567
```

The hero/footer/pre-order buttons and the WhatsApp handoff all use this one value.

## 2. Add the real product photos (two colours)

The product section has **two colour variants — Black and Cream** — each showing a drop-in **illustration** until you add real photos.

1. Save your two photos next to `index.html`, named exactly:
   - `band-black.jpg`
   - `band-cream.jpg`
   (Square ~1000×1000 on a dark background looks best.)
2. In `index.html`, find the comment `<!-- ===== PRODUCT PHOTO SLOTS` in the product section.
3. In each `.variant` block, **uncomment** the `<img ... >` line and **delete** the `<svg>…</svg>` illustration right below it.

The colour switch on the page (and in the pre-order form) already toggles between the two — so once both photos are in, clicking Black/Cream swaps the real images.

> Note: only **your own** product photos should go here. Don't use other brands' marketing images.

## 3. Other placeholders to replace

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
