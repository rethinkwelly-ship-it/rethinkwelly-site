# ReThinkWelly landing page (and reusable template)

A single-file, high-conversion landing page. No framework, no build step, no external
dependencies. Open `index.html` in any browser and it works. It also doubles as a template:
everything business-specific is isolated so the next business is a clone-and-swap.

> Note on style: no em dashes are used anywhere in this project, by design.

## Files

```
index.html        The entire page (HTML + CSS + JS inline)
images/           Placeholder before/after renders, IG tiles, and the hero background
README.md         This file
canva-prompt.md   A prompt to paste into Canva Code for a second take
```

## Fonts

The page loads two Google Fonts to match the ReThinkWelly wordmark: **Playfair Display**
(the serif in "ReThink" and the italic accent words) and **Archivo** (the bold sans in
"Welly." and all body text). They are requested from `fonts.googleapis.com`. If you would
rather have zero external requests, self-host the two families and swap the `<link>` in the
`<head>` for local `@font-face` rules. System fallbacks are already in place, so the page
still reads correctly if the fonts fail to load.

## What to change for ReThinkWelly (before going live)

1. **Images are already the real renders.** `images/` holds the three before/after pairs
   (`courtenay-*.jpg`, `hnry-*.jpg`, `leftbank-*.jpg`), the Wellington cable-car hero
   (`welly-hero.jpg`), plus the original full-resolution PNGs. To add a new project, drop in a
   matching `slug-before.jpg` / `slug-after.jpg` pair (16:9 works best) and copy one
   `.ba-item` block in the gallery markup.
2. **Confirm the links.** Search `index.html` for these and set the real values:
   - LinkedIn: `https://www.linkedin.com/company/rethinkwelly` (confirm the exact company URL).
   - Email: `rethinkwelly@gmail.com` (set your real contact address; it appears in the header,
     hero, get-involved links, form fallback, and footer).
3. **Real counter numbers.** In the "Mission + proof" section, update `data-count` on the three
   stats (spaces reimagined / ideas submitted / community following).
4. **Wire the form.** See "Submit-a-space form" below.
5. **Connect the live Instagram feed.** See "Instagram" below (optional; the page works without it).

All edit points are marked in the code with `EDIT HERE` comments.

## Instagram: from placeholder carousel to the live feed

**Already wired.** The live `@rethinkwelly` Behold feed is embedded in the Instagram section
(feed ID `HHxScaNkl0G6g5LczZbP`). One thing to know: Behold only renders the feed on domains
you have allowed, so **it shows nothing on `localhost` or a preview URL**. Once the site is live:
add your domain (the Netlify URL and `rethinkwelly.com`) under **Allowed domains** in the Behold
dashboard, and the feed appears. You can also restyle it (grid vs carousel, gaps, rows) from there.
To point at a different account later, swap the `feed-id` on the `<behold-widget>` tag.

The notes below are the original setup reference, in case you ever need to reconnect.

To auto-sync a live `@rethinkwelly` feed from scratch, use a free embed widget. **Behold** is the
cleanest; here is the exact flow.

**Step 0 (one-time): make the Instagram account a Professional account.** Behold (and every
service that uses Instagram's official API) needs this. It is free and takes a minute, and the
account stays public and looks the same:
- In the Instagram app: **Settings and privacy > Account type and tools > Switch to
  professional account** and pick **Creator** (or Business). That is all.

**Step 1: create the feed at Behold.**
1. Go to **[behold.so](https://behold.so)** and sign up (free tier is fine).
2. Click **Connect Instagram** and log in as `@rethinkwelly` to authorise it. (You do this on
   Behold's site, logged in as the account owner. It is not something the developer can do for
   you, since it needs the account's own login.)
3. Behold creates a feed and gives you a **feed ID** (a short string) and an embed snippet.

**Step 2: drop it into the page.** In `index.html`, find `INSTAGRAM FEED SLOT`. Just below it
are two commented lines. Uncomment them, paste your feed ID, then delete the
`<div class="carousel">...</div>` block and the `<div class="dots">` line under it:

```html
<script type="module" src="https://w.behold.so/widget.js"></script>
<behold-widget feed-id="PASTE_YOUR_BEHOLD_FEED_ID"></behold-widget>
```

That is it. New posts now appear automatically. The section title still links to the profile.
Behold lets you style the widget (grid, carousel, gaps) from its dashboard.

**SnapWidget alternative:** [snapwidget.com](https://snapwidget.com) works similarly and can
sometimes connect a personal (non-Professional) account. It hands you an `<iframe>` snippet;
paste that into the same slot instead. It shows a small free-tier badge.

Trade-off: a widget auto-syncs new posts but adds one third-party script and (on free tiers) a
small "powered by" mark. The built-in carousel has neither, but you swap its images by hand.
Either is fine; the page looks complete today either way.

## Submit-a-space form

**Wired for Netlify Forms.** The form is set up with `data-netlify="true"`, a hidden `form-name`
field, and a honeypot for spam. Once the site is deployed to Netlify, submissions appear
automatically in your Netlify dashboard under **Forms** (no endpoint, no third party). You will
also want to turn on **email notifications** there so a new submission pings `rethinkwelly@gmail.com`
(Netlify: Site settings > Forms > Form notifications > add an email notification).

Notes:
- Netlify detects the form by scanning the deployed HTML, so this works even for a drag-and-drop
  static deploy. Nothing else to configure.
- After deploy, do one test submission to confirm it shows up under Forms.
- Keep the form short. Three fields plus email is deliberate; every extra field lowers conversion.

If you ever move off Netlify, swap the form for [Formspree](https://formspree.io): set the form's
`action` to your Formspree URL and remove the `data-netlify` attribute and the hidden fields.

## Deploy

It is just static files, so anything works:

- **Netlify (drag and drop):** go to [app.netlify.com/drop](https://app.netlify.com/drop) and drag
  the whole `ReThinkWelly` folder in. Live in seconds. Then point `rethinkwelly.com` at it.
- **GitHub Pages:** push the folder to a repo, enable Pages on the `main` branch root.
- **Any host:** upload `index.html` and the `images/` folder to your web root.

Local preview: from this folder run `python3 -m http.server 8777` and open
`http://localhost:8777`. (Opening `index.html` directly works too.)

## Reusing this as a template for another business

1. Copy the whole folder.
2. Edit the `:root` tokens at the top of the `<style>` block (brand colour, ink, fonts, radius).
3. Replace the copy in the `EDIT HERE` blocks and the images in `images/`.
4. Update the social links and the form endpoint.
5. Paste that business's Instagram widget into the feed slot (or swap the `ig-*` tiles).

The structure (hero, mission + proof, how it works, before/after gallery, Instagram, submit, footer)
suits most simple, visual, single-goal businesses.

## Accessibility and performance notes

- Fully self-contained: no CDN, no web fonts, no tracking. Fast, and works offline.
- The before/after sliders and carousel are keyboard and touch accessible.
- All motion respects `prefers-reduced-motion` (it degrades to static).
