# ReThinkWelly website: complete handover guide

---

## For the owner (read this bit first)

This file has everything needed to look after the ReThinkWelly website.

**How to use it:** start a new chat with your AI assistant, attach this file, and say:

> Read this file in full and follow the instructions in it. Start with the setup walkthrough.

The AI will then walk you through the one-time setup, one step at a time, and after that it
can make changes to the website whenever you ask.

You will need these logins handy (do not paste passwords into the chat, just log in when
the AI asks you to):

- **GitHub** (the `rethinkwelly-ship-it` account): where the website's code lives
- **Netlify**: hosts the website and collects form submissions
- **Behold** (behold.so): powers the live Instagram feed on the site
- **Squarespace**: where the domain name is registered (you should not need to change anything)

---

## For the AI assistant: your instructions

You are helping the owner of the ReThinkWelly website look after it. **The owner is not
technical.** Follow these rules throughout:

- Explain everything in plain English. No jargon, or explain it when you must use it.
- Go **one step at a time**. Wait for the owner to confirm each step is done before moving on.
- If a step fails, help troubleshoot before continuing.
- **Never ask the owner to paste a password, API key or token into the chat.** Tell them to
  log in directly on the relevant website instead.
- Before you push any change to the website, tell the owner exactly what will change on the
  live site, and wait for a clear yes.
- Follow every rule in Parts 3 to 5 of this file.

**Your first job is the setup walkthrough in Part 1.** Start it now. Once setup is done,
tell the owner they can ask for changes any time, and give them a few examples (Part 7).

---

## Part 1: Setup walkthrough (one time)

Take the owner through these steps in order.

**Step 1: Check the website is live.**
Ask the owner to open https://rethinkwelly.com and confirm the site loads.

**Step 2: GitHub access.**
The code is in the GitHub repo **rethinkwelly-ship-it/rethinkwelly-site**
(https://github.com/rethinkwelly-ship-it/rethinkwelly-site).
Ask the owner to log in to github.com as `rethinkwelly-ship-it` and open the repo link to
confirm they can see it. If they use a different GitHub account, they need to be added as a
collaborator on the repo (Settings, Collaborators) by whoever controls `rethinkwelly-ship-it`.

**Step 3: Connect GitHub to this AI tool.**
Guide the owner through *your own platform's* way of connecting to GitHub (an integration,
connector or app install), and giving it read and write access to the `rethinkwelly-site`
repo. You know your platform best, so give precise click-by-click directions. If your
platform cannot write to GitHub, say so plainly and explain the alternative: you prepare the
exact edit, and the owner applies it on github.com using the pencil (edit) icon on the file,
then "Commit changes".

**Step 4: Confirm you can see the code.**
Once connected, open the repo yourself and confirm you can read `index.html` and this file
(`HANDOVER.md`). Tell the owner it worked.

**Step 5: Netlify check.**
Ask the owner to log in at https://app.netlify.com and open the **rethinkwelly** site.
Confirm with them that:
- The latest deploy shows **Published** (green).
- Under **Forms**, a form called **get-involved** is listed.
- Under **Forms, Form notifications**, there is an **email notification** for the
  `get-involved` form going to **rethinkwelly@gmail.com**. If not, walk them through adding
  one (Add notification, Email notification, choose the `get-involved` form).

**Step 6: Test the form.**
Ask the owner to go to https://rethinkwelly.com, scroll to **Get Involved**, choose "Local",
fill it in with test details and submit. Then check it appears in Netlify under Forms and
that the notification email arrived. They can delete the test submission afterwards.

**Step 7: Behold (Instagram feed) check.**
Ask the owner to look at the Instagram section on the live site. If it shows their posts,
done. If it is empty, walk them through logging in to behold.so, opening their feed's
settings, and adding these to **Allowed domains**: `rethinkwelly.com`,
`www.rethinkwelly.com`, `rethinkwelly.netlify.app`.

**Step 8: Done.**
Tell the owner setup is complete and explain, simply, how changes work from now on:
they ask, you show what will change, they say yes, you push, and the live site updates
in about a minute.

---

## Part 2: How the website works

- **Live site:** https://rethinkwelly.com
- **Code:** GitHub repo `rethinkwelly-ship-it/rethinkwelly-site` (public)
- **Hosting:** Netlify, connected to the repo. **Every push to the `main` branch goes live
  automatically within about a minute.** There is no separate test site, so treat `main` as live.
- **Domain:** registered at Squarespace, with DNS pointing to Netlify. Do not touch DNS.

The site is deliberately simple: **four plain HTML pages, no framework, no build step.**
Each page carries its own copy of the CSS (in `<style>`) and JS (in `<script>`), so a
style change must be made in all four files to stay consistent.

```
index.html                         Home: hero, Instagram feed, Get Involved strip
visions.html                       Visions: How it works (01/02/03), all before/after sliders, Instagram
about.html                         About: mission, roadmap, independence note
get-involved.html                  Get Involved: Join the collective cards + the get-involved form
images/                            Optimised images used by the site (.jpg)
netlify.toml                       Netlify settings (publish folder, caching, security headers)
favicon.ico, favicon-*.png,
apple-touch-icon.png               Browser tab and phone home-screen icons
HANDOVER.md                        This guide
README.md                          Older technical notes
reference-instagram-carousel.html  Unused reference snippet. Ignore it.
```

Every page shares the same header (Visions, About, Get Involved) and footer.
The sections below now live on these pages: 2 and 7 on Home; 4, 6 and 7 on Visions
(sliders live only on Visions); 3 and 5 on About; 8 and 9 on Get Involved.
Original section list (each is a `<section>` with a comment header):

1. Header: wordmark, Instagram and LinkedIn icons, "Get Involved" button
2. Hero: main headline, subtext, two buttons, Wellington cable-car photo
3. Mission
4. How it works: 3 numbered steps
5. Roadmap: "What is next for ReThinkWelly?", 5 items with icons
6. Gallery: before/after sliders (`id="gallery"`)
7. Instagram feed: live, via Behold
8. Join the collective: 4 audience quote cards (`id="collective"`)
9. Get Involved form (`id="submit"`)
10. Footer

Editable text is marked in the HTML with `EDIT HERE` comments.

---

## Part 3: Brand rules (follow on every change)

- **Never use em dashes (the long dash).** Use commas or full stops, or rewrite the sentence.
- **Say "architectural visualisation", never "AI",** when describing how the renders are made.
- **Te reo Māori is part of the voice:** Te Whanganui-a-Tara (Wellington), Kia ora, the waka,
  Aotearoa. Keep it, and keep macrons where they appear.
- **Tone:** bold, visionary, collaborative, local, proactive. Short sentences. No jargon.
- **Colours** are CSS variables at the top of `<style>`. Use them, never add new colours:
  `--brand` `#FEE05A` (yellow), `--ink` `#121110` (near black), `--paper` (white).
- **Fonts:** Archivo (bold sans, headings and body) and Playfair Display (serif, used in
  italic for accent words). The signature style is one italic serif word inside a bold
  heading: `Join the <span class="ser">collective.</span>`
- **Highlighting a phrase on a light background:** wrap it in `<span class="hl">...</span>`
  (yellow highlighter effect). Never use yellow *text* on white, it is unreadable.
  Yellow text is only for dark sections.
- **Wordmark:** `<span class="wm"><i>Re</i>Think<b>Welly.</b></span>`. Do not restyle it.

---

## Part 4: How to make common changes

**Change some words:** find the text in `index.html` and change only the words. Keep the
HTML tags around them exactly as they are.

**Add a new before/after project:**
1. The owner provides two images: before and after, same size, landscape 16:9
   (1600 x 900 is ideal), each under about 400 KB. Name them `slug-before.jpg` and
   `slug-after.jpg` (for example `kent-terrace-before.jpg`) and add them to `images/`.
2. In the gallery section (in `visions.html`, the only page with sliders), copy one whole `<div class="ba-item reveal">...</div>` block,
   paste it after the others, and update: both image paths, the `alt` text, the
   `aria-label`, the location name (`.loc`), the description (`.desc`) and the question
   underneath (`.ba-prompt`).

**Replace an image:** keep the same filename and the same shape, so nothing else needs to
change. Compress big photos to well under 500 KB first.

**Instagram feed:** it is a Behold widget (`<behold-widget feed-id="...">`) and updates
itself from Instagram. Its layout and style are changed in the Behold dashboard, not in the
code. Do not edit the widget code unless the feed is being replaced.

**The Get Involved form** (Netlify Forms, form name `get-involved`):
- An "I am a..." dropdown reveals one of three groups of fields (`group-local`,
  `group-creative`, `group-business`), controlled by a small script near the bottom of the file.
- **Never remove** `data-netlify="true"`, the hidden `form-name` input, or the hidden
  `bot-field` honeypot. The form stops working without them.
- Every field must be written in the HTML itself, not created by JavaScript, or Netlify will
  not save it. To add a field, copy an existing `<div class="field">` inside the right group
  and give it a new unique `id` and `name`.
- Submissions appear in Netlify under **Forms**; email notifications are set up there too.

---

## Part 5: Rules for changing the site

- **Make small, targeted edits.** Never rewrite or regenerate the whole `index.html`.
  Change only what was asked.
- **Keep it plain static files.** No frameworks, packages or build tools, and no new pages
  unless the owner explicitly asks.
- **Before every push,** describe in plain English exactly what will change on the live
  site, and wait for a yes.
- **Small text or image changes:** commit straight to `main` (live in about a minute).
- **Bigger changes** (new sections, layout changes, anything touching the form or the
  scripts): make them on a new branch and open a pull request. Netlify then creates a
  **deploy preview** link. Send it to the owner to check before merging into `main`.
- **Clear commit messages,** for example "Update hero subtext" or "Add Kent Terrace project".
- **Check phones.** Most visitors come from Instagram on mobile. Nothing should overflow or
  need sideways scrolling on a narrow screen.
- **Never commit passwords, keys or tokens.** The repo is public.

---

## Part 6: Troubleshooting

| Problem | What to do |
|---|---|
| Change pushed but site has not updated | Wait 2 minutes, then hard refresh (Cmd+Shift+R). If still old, check Netlify, Deploys: the latest should be green "Published". If it failed, open it and read the error. |
| Something broke after a change | Fastest fix: Netlify, Deploys, click the last good deploy, **Publish deploy**. This restores it instantly. Then revert the bad commit in GitHub so the next push does not bring it back. |
| Form submissions not arriving | Check Netlify, Forms: is `get-involved` listed and receiving? Then check Form notifications has the email set. Check the spam folder. |
| Instagram section is empty | Behold dashboard: add the domains listed in Part 1, Step 7, to Allowed domains. |
| Deploy says "unrecognized Git contributor" | Only happens if the repo is made private. Keep the repo public, then retry the deploy. |
| Browser tab icon still old | Browsers cache icons. Open the site in a fresh tab or private window. |

---

## Part 7: Example requests the owner can make

- "Change the hero subtext to: ..."
- "Add a new before/after project for Kent Terrace. Here are the two images."
- "Update the roadmap: move Street Interviews to say it has launched."
- "Swap the cable car photo at the top for this one."
- "Add a new question to the Local form: How often do you pass this space?"
- "Show me what submissions have come in" (the AI will direct them to Netlify, Forms).

---

## Quick reference

| What | Where |
|---|---|
| Live site | https://rethinkwelly.com |
| Code | https://github.com/rethinkwelly-ship-it/rethinkwelly-site |
| Hosting, forms, rollbacks | https://app.netlify.com (site: rethinkwelly) |
| Instagram feed settings | https://behold.so |
| Domain registration | Squarespace Domains (leave alone) |
| Contact email | rethinkwelly@gmail.com |
| Instagram | https://instagram.com/rethinkwelly |
| LinkedIn | https://www.linkedin.com/company/rethinkwelly |
