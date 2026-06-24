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

## 2. Other placeholders to replace

- **Instagram handle** — in the footer: `https://instagram.com/your_handle_here`.
- **Product photos** — tasteful SVG/gradient placeholders are used for now; swap in real images when ready.
- **OG image** — the `og:image` meta points to a placeholder URL; host a 1200×630 image and update it for nice social previews.

## 3. Optional: also save orders to Formspree (disabled by default)

Orders go straight to WhatsApp. If you also want a copy saved server-side,
create a free [Formspree](https://formspree.io) form and set:

```js
const FORMSPREE_ENDPOINT = "https://formspree.io/f/xxxxxxxx";
```

Leave it as `""` to keep it off. It's fire-and-forget and never blocks the WhatsApp step.

## 4. Deploy (Netlify Drop)

1. Go to <https://app.netlify.com/drop>.
2. Drag the folder containing `index.html` (or just the file) onto the page.
3. You get a live URL instantly. Optionally connect a custom domain in Site settings.

That's it — no other steps needed.
