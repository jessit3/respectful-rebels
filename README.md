# Respectful Rebels: Project Finder + Rebel Quest

Two pages, ready to go live for free on GitHub Pages at respectfulrebels.com.

| Page | Address once live | What it is |
|---|---|---|
| `index.html` | respectfulrebels.com | The parent quiz "Find Your Teen's First Real Project" with the sign-up and the visual results page |
| `quest/index.html` | respectfulrebels.com/quest/ | The teen's Rebel Quest game. Collects nothing; everything stays on the device |

`CNAME` tells GitHub the domain. `.nojekyll` tells GitHub to serve the files as they are.

---

## Part 1: Put it online (about 15 minutes, free)

1. Sign in to GitHub as **jessit3**. Top right **+** → **New repository**.
   - Name: `respectful-rebels`
   - Public (GitHub Pages is free for public repositories)
   - Tick "Add a README file" → **Create repository**
2. In the new repository: **Add file** → **Upload files**. Drag in everything from this folder, **including the `quest` folder, `CNAME` and `.nojekyll`**. (On a Mac, press Cmd + Shift + . in Finder to see `.nojekyll`.) → **Commit changes**.
3. **Settings** → **Pages**. Under "Build and deployment": Source **Deploy from a branch**, Branch **main**, folder **/ (root)** → **Save**.
4. While you wait for the domain, your site works at `https://jessit3.github.io/respectful-rebels/`. Test it on your phone.

## Part 2: Connect respectfulrebels.com

At the company where you bought respectfulrebels.com, open its DNS settings and add:

| Type | Name / Host | Value |
|---|---|---|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |
| CNAME | www | jessit3.github.io |

Check these against GitHub's own guide ("Managing a custom domain for your GitHub Pages site") before saving, and remove any old "parking" A records. Then in GitHub **Settings → Pages**, type `respectfulrebels.com` under Custom domain, wait for the green tick (minutes to 24 hours), and tick **Enforce HTTPS**.

## Part 3: Send sign-ups to FEA Create

Until this is done, the quiz works but sign-ups go nowhere (safe for testing with friends).

1. In FEA Create: **Automation → Workflows → Create workflow → Start from scratch**.
2. Trigger: **Inbound Webhook**. Copy the webhook URL it gives you. (Check whether FEA Create charges for this trigger. If it does, tell Claude and we'll use a form instead.)
3. Give that URL to Claude, who will put it in the quiz and rebuild. The quiz sends: first name, email, consent, result name, the tag `freebie-project-quest`, one result tag (`project-quest-spark`, `-player` or `-dreamer`), and the personal results link. It never sends the teen's support-needs answer.
4. In the workflow, add actions: **Create/Update Contact** (map first name and email), **Add Tag** (both tags), save the result and results link to custom fields, then send the delivery email.

## Part 4: Before you share it

- [ ] Webinar time and registration link (Tuesday, December 29)
- [ ] Cohort link
- [ ] Webhook URL from Part 3
- [ ] Take the quiz on your phone 3 times, once for each result
- [ ] Open the Rebel Quest from the results page on your phone and play to Mission 2

---

## Part 5: Using Google AI Studio (free) to change things later

Google AI Studio's **Build** mode can import this repository, let you change it by chatting, and sync changes back to GitHub. Don't ask it to rebuild from scratch: these pages are finished and tested, and AI Studio defaults to rewriting apps in React.

1. Go to aistudio.google.com → **Build**.
2. In the prompt box: **+** → **Import from GitHub** → choose `respectful-rebels`.
3. Paste this first, every time:

```text
This repository is a finished static website for GitHub Pages: index.html (a parent quiz) and quest/index.html (a teen game). Each is one self-contained HTML file with its own CSS and JavaScript.
Rules for every change:
- Keep it plain HTML, CSS and JavaScript. Do not convert it to React, add a build step, a server or any npm packages.
- Change only what I ask. Keep all existing features, text and layout unless I say otherwise.
- Keep it working on phones first and on laptops.
- The teen game must never send data anywhere. Everything stays in the browser (localStorage).
- Use American English. Colors: background #FAF8F6, panels #ded2eb, accent #b3c9f1, buttons #037A8C with white text, decoration #05ABC4, highlights #b180bd, text #3c2415 (never pure black). Fonts: Montserrat for headings, Nunito for body.
Confirm you understand, then wait for my first change.
```

4. Ask for one change at a time, for example: *"In quest/index.html, add a new interest tile called 'Cooking and food' with its own illustration."* Use **annotation mode** to point at the exact part of the page.
5. When it looks right, use the **GitHub** sync in Settings to push the change. GitHub Pages updates the live site within a few minutes.

### For the December 29 live build

Teens copy their **Remix prompt** from the Rebel Quest (Remix tab). In AI Studio Build, start a **new** app (not your website) and paste:

```text
Build a single-page, phone-friendly web app: a personal project quest for a teenager, using only HTML, CSS and JavaScript in one file. Picture-led, playful, bite-sized, with three "moves" per mission (say it, make it, ask someone) and badges. It must collect no personal data and save only in the browser. Here is the teen's remix brief:
[paste the Remix prompt here]
```

Google lets you deploy up to two AI Studio apps to Cloud Run free. Keep those for later; the website itself lives on GitHub Pages.
