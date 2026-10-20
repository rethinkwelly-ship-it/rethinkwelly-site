# ReThinkWelly website: handover guide

**Read this whole file before making any change to this repo.** It is written for an AI
assistant working on the site on behalf of the owner, who is not a developer. Explain what
you change in plain English, and confirm with the owner before pushing anything.

---

## 1. What this is

- **Live site:** https://rethinkwelly.com
- **Repo:** https://github.com/rethinkwelly-ship-it/rethinkwelly-site (public)
- **Hosting:** Netlify, connected to this repo. **Every push to `main` goes live
  automatically within about a minute.** There is no staging site, so treat `main` as live.
- **Domain:** `rethinkwelly.com` is registered at Squarespace, with DNS pointing at Netlify.
  Do not touch DNS.

## 2. How the site is built

It is deliberately simple: **one HTML file, no framework, no build step.**

```
index.html                       The whole site: HTML, CSS (in <style>) and JS (in <script>)
images/                          Optimised images used by the site (.jpg)
netlify.toml                     Netlify settings (publish folder, cache and security headers)
favicon.ico, favicon-*.png,
apple-touch-icon.png             Browser tab and home-screen icons
README.md                        Longer technical notes
reference-instagram-carousel.html  Unused reference snippet. Ignore it.
```

Page sections, top to bottom (each is a `<section>` with a comment header in `index.html`):

1. Header (wordmark, Instagram and LinkedIn icons, "Get Involved" button)
2. Hero (headline, subtext, two buttons, cable-car photo)
3. Mission
4. How it works (3 numbered steps)
5. Roadmap: "What is next for ReThinkWelly?" (5 items with icons)
6. Gallery: before/after sliders (`id="gallery"`)
7. Instagram feed (live, via Behold)
8. Join the collective (4 audience quote cards, `id="collective"`)
9. Get Involved form (`id="submit"`)
10. Footer

Editable copy is marked in the HTML with `EDIT HERE` comments.

## 3. Brand rules (follow these on every change)

- **Never use em dashes (the long dash).** Use commas, full stops or rewrite the sentence.
- **Say "architectural visualisation", never "AI",** when describing how renders are made.
- **Te reo Māori is part of the voice:** Te Whanganui-a-Tara (Wellington), Kia ora, the waka,
  Aotearoa. Keep it, and use macrons correctly where they already appear.
- **Tone:** bold, visionary, collaborative, local, proactive. Short sentences. No jargon.
- **Colours** are CSS variables at the top of `<style>`. Use them, never hard-code new colours:
  - `--brand` `#FEE05A` (yellow), `--ink` `#121110` (near black), `--paper` (white)
- **Fonts:** Archivo (bold sans, for headings and body) and Playfair Display (serif, used in
  italic for accent words). The signature move is one italic serif word inside a bold heading:
  `Join the <span class="ser">collective.</span>`
- **Accent highlights:** to highlight a phrase on a light background, wrap it in
  `<span class="hl">...</span>` (yellow highlighter). Never use yellow *text* on a white
  background, it is unreadable. Yellow text is only for dark sections.
- **Wordmark:** `<span class="wm"><i>Re</i>Think<b>Welly.</b></span>`. Do not restyle it.

## 4. How to make common changes

**Change words:** find the text in `index.html` and edit only that text. Keep the HTML tags
around it exactly as they are.

**Add a new before/after project:**
1. Add two images to `images/`, named like `slug-before.jpg` and `slug-after.jpg`.
   Both must be the same size, landscape 16:9 (1600 x 900 is ideal), under ~400 KB each.
2. In the gallery section, copy one whole `<div class="ba-item reveal">...</div>` block,
   paste it below the others, and update the two image paths, the `alt` text, the
   `aria-label`, the location name (`.loc`), the description (`.desc`) and the question
   (`.ba-prompt`).

**Replace an image:** keep the same filename and the same proportions, so nothing else
needs to change. Compress large photos to well under 500 KB first.

**Instagram feed:** it is a Behold widget (`<behold-widget feed-id="...">`). It updates
itself from the Instagram account. Layout and style are changed in the Behold dashboard,
not in this code. Do not edit the widget code unless the feed itself is being replaced.

**The Get Involved form** (handled by Netlify Forms, form name `get-involved`):
- It has an "I am a..." dropdown that reveals one of three field groups
  (`group-local`, `group-creative`, `group-business`), controlled by a small script.
- **Do not remove** `data-netlify="true"`, the hidden `form-name` input, or the hidden
  honeypot field (`bot-field`). The form stops working without them.
- Every field must exist in the HTML itself (not created by JavaScript), or Netlify will
  not record it. To add a field, copy an existing `<div class="field">` inside the right
  group and give it a new unique `id` and `name`.
- Submissions appear in Netlify under **Forms**, and email notifications are set up there.

## 5. Rules for working on this repo

- **Make small, targeted edits.** Never rewrite or regenerate the whole `index.html`.
  Change only what was asked.
- **Keep it a single static file.** Do not add frameworks, npm packages, build tools,
  or new pages without the owner explicitly asking.
- **Before every push:** tell the owner in plain English exactly what will change on the
  live site, and wait for a yes.
- **Small text or image changes:** commit straight to `main` (it goes live in a minute).
- **Bigger changes** (new sections, layout changes, anything touching the form or
  scripts): put them on a new branch and open a pull request. Netlify then builds a
  **deploy preview** link so the owner can check it before merging to `main`.
- **Write clear commit messages,** e.g. "Update hero subtext" or "Add Kent Terrace project".
- **Check mobile.** Most visitors arrive from Instagram on a phone. Nothing should overflow
  or need sideways scrolling on a narrow screen.
- **Never commit passwords, API keys or tokens.** This repo is public.
- **If something breaks:** the last working version can be restored by reverting the bad
  commit on `main`. Netlify can also roll back instantly: Deploys, pick an earlier
  successful deploy, "Publish deploy".

## 6. Things that live outside this repo

These are changed in their own dashboards, not in code:

| What | Where |
|---|---|
| Form submissions and email notifications | Netlify, Forms |
| Domain, HTTPS, deploys, rollbacks | Netlify |
| Instagram feed style and allowed domains | Behold (behold.so) |
| Domain DNS records | Squarespace Domains (leave alone) |

## 7. Starting a new AI session (for the owner)

Paste this at the start of a new chat, then say what you want changed:

> You are helping me update my website. The code is in the GitHub repo
> rethinkwelly-ship-it/rethinkwelly-site. Connect to it and read HANDOVER.md in full before
> doing anything, and follow its rules. I'm not technical, so explain things simply. Make
> only the change I ask for, show me what will change, and wait for my OK before pushing.
