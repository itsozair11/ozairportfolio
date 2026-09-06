# Ozair Kamran — Portfolio

A single-page portfolio for a pre-dental student who also writes software. Seven full-screen sections, a 3D project carousel, and a dental radiograph light box — built as one HTML file with no framework, no build step, and no dependencies.

**Live:** [itsozair11.github.io](https://itsozair11.github.io) · **Contact:** ozairkamran11@gmail.com

```
Pre-Dental  ·  Biology  ·  Computer Science
University of Texas at Dallas — B.S. Computer Science, Minor in Biology, Class of 2027
```

---

## Contents

- [What's in it](#whats-in-it)
- [How it works](#how-it-works)
- [Getting it running](#getting-it-running)
- [File structure](#file-structure)
- [Adding your photos](#adding-your-photos)
- [Editing the content](#editing-the-content)
- [Design system](#design-system)
- [Deploying to GitHub Pages](#deploying-to-github-pages)
- [Custom domain](#custom-domain)
- [Browser support & accessibility](#browser-support--accessibility)
- [Roadmap](#roadmap)

---

## What's in it

Seven sections, each a full-screen "scene" that zooms in and out as you move between them.

| # | Section | What's there |
|---|---------|--------------|
| 01 | **Home** | Name, UTD wordmark, and a green splash screen that collapses into a circle wipe on load |
| 02 | **About** | Photo, bio, and four skill groups — chairside & patient care, clinical foundation, languages, tools |
| 03 | **Dentistry + CS** | Why both disciplines, side by side, plus every completed course in two columns |
| 04 | **Experience** | Roles with dates and outcomes, hover-highlighted rows |
| 05 | **Projects** | Three projects on a rotating 3D ring you can drag, with full write-ups and photo strips |
| 06 | **Beyond** | Radiograph light box: volunteering, research, shadowing, leadership, manual dexterity |
| 07 | **Contact** | Email, LinkedIn, GitHub, résumé download |

### The two interactive pieces

**Projects — a 3D carousel.** Cards are laid out on a ring in real 3D space using CSS `transform-style: preserve-3d`. The radius is computed with trigonometry from the card width and the angle between cards, so the ring never overlaps itself no matter how many projects are in the array. Drag it with a mouse or finger, use the arrow keys, or hit the ‹ › buttons. Click the front card to open the full write-up.

**Beyond — a radiograph light box.** Five film panels mounted in a viewer. Hovering one switches on the backlight behind it — the panel lifts, a soft glow bleeds through, and the cover photo fades up from underneath. Click to open the entry with its own photo gallery.

---

## How it works

No React, no bundler, no `npm install`. One `index.html` containing the markup, the styles, and about 400 lines of vanilla JavaScript. Open it in a browser and it runs.

**Section navigation** — scroll wheel, arrow keys, swipe, the tick marks on the right edge, or the full-screen menu. All of it routes through one `goTo(i)` function with an animation lock so transitions can't stack up.

**Scroll that behaves.** The wheel normally flips between sections, but if your cursor is over a panel that still has content below the fold, the panel scrolls instead and the section stays put. Same logic for touch. The site checks what's under the pointer before deciding.

**Photos that fail gracefully.** Every image is loaded speculatively. If the file isn't in `photos/` yet, that frame is removed and the strip hides itself — no broken-image icons, no empty boxes. Add photos one at a time and each appears the moment it exists.

**Keyboard map**

| Key | Does |
|-----|------|
| <kbd>↓</kbd> <kbd>↑</kbd> | Next / previous section |
| <kbd>→</kbd> <kbd>←</kbd> | Next / previous section — *or* spin the carousel while on Projects |
| <kbd>Enter</kbd> / <kbd>Space</kbd> | Open the focused project card or film panel |
| <kbd>Esc</kbd> | Close an open panel or the menu |
| <kbd>Tab</kbd> | Move through cards and panels with a visible focus ring |

---

## Getting it running

```bash
git clone https://github.com/itsozair11/itsozair11.github.io.git
cd itsozair11.github.io
open index.html          # macOS — or just double-click the file
```

For a local server (optional, but closer to how it behaves when hosted):

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

---

## File structure

```
/
├── index.html               the entire site — markup, styles, and scripts
├── pic01.jpg                portrait used on the About section
├── OzairKamranResume.pdf    linked from Contact; keep this filename when you swap it
├── photos/                  project and Beyond photos (see below)
│   └── README.txt           the filenames the site looks for
├── DEPLOY.md                short deploy notes
└── README.md                this file
```

---

## Adding your photos

Drop images into `photos/` using these names. Anything missing is skipped, so you can fill them in over time.

**Project galleries** — appear when a project is opened. Landscape, roughly 4:3.

```
er-medsys-1.jpg      er-medsys-2.jpg      er-medsys-3.jpg
dental-medsys-1.jpg  dental-medsys-2.jpg  dental-medsys-3.jpg
eeg-analyzer-1.jpg   eeg-analyzer-2.jpg   eeg-analyzer-3.jpg
```

**Beyond panels** — each panel takes a `-cover` image (shown behind the panel, cropped to portrait) plus gallery photos.

```
volunteering-cover.jpg   volunteering-1.jpg   volunteering-2.jpg   volunteering-3.jpg
research-cover.jpg       research-1.jpg       research-2.jpg       research-3.jpg
shadowing-cover.jpg      shadowing-1.jpg      shadowing-2.jpg
leadership-cover.jpg     leadership-1.jpg     leadership-2.jpg
dexterity-cover.jpg      dexterity-1.jpg      dexterity-2.jpg      dexterity-3.jpg
```

Keep files under ~400 KB each so the page stays quick. The covers sit at low opacity until you hover, so slightly brighter images read better than dark ones.

---

## Editing the content

Everything lives in `index.html`. Search for these anchors:

### Projects — search `const PROJECTS`

An array near the bottom of the file. Add, remove, or reorder freely; the carousel recalculates its geometry from however many entries it finds.

```js
{
  name:   'ER MedSys',
  tag:    'Patient Records & Triage',   // small label at the top of the card
  year:   'Spring 2026',
  role:   'Schema design, validation layer',
  status: 'Completed',
  stack:  ['SQL', 'Python', 'SQLite'],  // chips on the card
  short:  'One or two lines shown on the card face.',
  detail: 'The full write-up. Basic HTML works — <strong>bold</strong> and <br><br> for paragraphs.',
  images: ['photos/er-medsys-1.jpg'],   // missing files are skipped
  link:   'https://github.com/itsozair11'
}
```

The link button relabels itself automatically — a `github.com` URL reads "View on GitHub," anything else reads "Open live site."

### Beyond panels — search `const BEYOND`

Same shape, one object per film panel:

```js
{
  label:  'Volunteering',                  // big text on the panel
  kind:   'Community service',             // small caption underneath
  cover:  'photos/volunteering-cover.jpg', // image behind the panel
  body:   'The write-up shown when the panel is opened.',
  images: ['photos/volunteering-1.jpg']
}
```

Five panels fit the mount cleanly on desktop; more will still work but will wrap.

### Everything else

Bio, skills, coursework, and job history are plain HTML. Each section opens with a comment banner you can search for:

| Search for | Section id | What you'll be editing |
|------------|-----------|------------------------|
| `SCENE 1 — ABOUT` | `#s1` | Bio paragraphs and the four skill-chip groups |
| `SCENE 2 — DENTISTRY` | `#s2` | The "Why both" copy and both coursework lists |
| `SCENE 3 — EXPERIENCE` | `#s3` | Job rows — company, dates, role, bullets |
| `SCENE 6 — CONTACT` | `#s6` | Links, email, phone |

To add a skill chip, copy a `<span class="chip">` line. Use `chip h` for an orange highlight or `chip d` for the clinical variant.

> **Adding or removing a whole section?** Update three places so navigation stays in sync: the `SCENES` and `NAMES` arrays in the script, the tick marks in `#snav`, and the menu items in `#menu`. The counter in the bottom-right corner is hardcoded — change `/ 07` too.

---

## Design system

UT Dallas colors, dark. Three typefaces, each with one job.

| Token | Value | Used for |
|-------|-------|----------|
| `--bg` | `#0b1610` | Page background |
| `--surf` | `#111f17` | Side panels, detail panels |
| `--acc` | `#E87722` | UTD orange — the software half of the site |
| `--grn` | `#154734` | UTD green — the splash screen |
| `--enam` | `#cfe3d6` | Enamel white — the clinical half |
| `--mut` | `#7b9e85` | Body copy, labels |

Every color is a CSS custom property in `:root` at the top of the file. Change one line and it propagates everywhere.

**Type:** Bebas Neue for display, Crimson Pro for body copy, DM Mono for labels and data. Loaded from Google Fonts — the only external request the site makes.

The two accents carry meaning rather than decoration: orange marks engineering work, enamel marks clinical work. The Dentistry section puts them side by side on purpose.

---

## Deploying to GitHub Pages

**1. Create the repo.** Name it exactly `itsozair11.github.io` and make it public. That exact name is what gives you the root domain instead of a subfolder.

**2. Upload the files.** Drag `index.html`, `pic01.jpg`, `OzairKamranResume.pdf`, and the `photos` folder into **Add file → Upload files**, then commit.

Or from the terminal:

```bash
git init
git add .
git commit -m "portfolio"
git branch -M main
git remote add origin https://github.com/itsozair11/itsozair11.github.io.git
git push -u origin main
```

**3. Turn on Pages.** Repo **Settings → Pages**, set the branch to `main`, save. Give it about a minute, then visit `https://itsozair11.github.io`.

Every push republishes within seconds. To edit later, change `index.html` and push again — there's nothing to rebuild.

---

## Custom domain

Buy the domain, then add these DNS records at your registrar:

| Type | Host | Value |
|------|------|-------|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |
| CNAME | www | itsozair11.github.io |

Then **Settings → Pages → Custom domain**, enter the domain, save, and tick **Enforce HTTPS**. DNS can take up to 24 hours to propagate.

---

## Browser support & accessibility

Tested in Chromium at 1440×900, 1366×768, and 390×844.

- **Responsive** — side panels collapse below 900px, the carousel and light box resize, and the custom cursor is disabled on touch devices where it makes no sense.
- **Short screens** — a `max-height` breakpoint tightens the dense panels so laptop users aren't scrolling through the About section.
- **Keyboard** — cards and panels are reachable by <kbd>Tab</kbd> with a visible focus ring, and openable with <kbd>Enter</kbd>.
- **Reduced motion** — `prefers-reduced-motion` collapses animations to near-instant.
- **Requires** CSS 3D transforms and Pointer Events. Works in current Safari, Chrome, Firefox, and Edge. Not built for IE.

---

## Roadmap

- [ ] Real photos in `photos/` for all three projects
- [ ] Fill in the Volunteering, Shadowing, and Manual Dexterity panels
- [ ] Individual repo links per project instead of the profile link
- [ ] Update the RDA certification card once registration is complete
- [ ] `og:image` and social preview tags

---

## License

Personal portfolio. The code is free to learn from; the content, résumé, and photographs are not for reuse.

<sub>Built by Ozair Kamran · Dallas, Texas</sub>
