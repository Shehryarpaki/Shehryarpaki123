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

## 2. Add the real H59 Max photo

The product section currently shows a drop-in **illustration** of the band. To use a real photo:

1. Save your photo next to `index.html` — name it `h59-max.jpg` (a square ~1000×1000 image on a dark or transparent background looks best).
2. In `index.html`, find the comment `<!-- ===== PRODUCT PHOTO SLOT` in the product/pricing section.
3. Uncomment the `<img ... src="h59-max.jpg" ...>` line and delete the `<svg>…</svg>` illustration below it (and the `<span class="media-note">` line).

That's it — your photo replaces the placeholder. You can add more photos the same way.

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
