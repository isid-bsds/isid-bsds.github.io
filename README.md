# isid-bsds.github.io

An **unofficial** website for the **Bachelor of Statistical Data Science (BSDS)** programme at the **Indian Statistical Institute (ISI), Delhi Centre**.

> This site is a student-run prototype. It is not the official ISI website. For official information, see the [ISI main site](https://www.isical.ac.in/), the [official BSDS programme page](https://www.isical.ac.in/~deanweb/bsds.html), and the [admission portal](https://admission.isical.ac.in/).

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Repository Structure](#repository-structure)
- [Tech Stack](#tech-stack)
- [Getting Started](#getting-started)
- [Deployment (GitHub Pages)](#deployment-github-pages)
- [Customising the Site](#customising-the-site)
  - [Hero images](#hero-images)
  - [News and Events](#news-and-events)
  - [Student Activities](#student-activities)
  - [Contacts](#contacts)
  - [Theme and colours](#theme-and-colours)
  - [Carousel timing](#carousel-timing)
- [Design and Accessibility Notes](#design-and-accessibility-notes)
- [Responsive Breakpoints](#responsive-breakpoints)
- [Contributing](#contributing)
- [Disclaimer](#disclaimer)

---

## Overview

The BSDS programme is a four-year Bachelor (Hons.) degree focused on statistical methodology, with emphasis on statistical machine learning, computational and classical statistics, and data analytics, built on rigorous training in statistics, probability and mathematics.

This repository hosts the static website that presents the programme at the Delhi Centre: an about section, programme facts, news and events, student activities and achievements, and contact details.

**Quick programme facts shown on the site**

| Item | Detail |
|---|---|
| Duration | Four years, Bachelor (Hons.) |
| Exit option | BSDS degree after three years |
| Fifth year | Optional; leads to an Integrated Master of Statistical Data Science |
| Seats per centre | 25 (as stated on the official programme page) |
| Eligibility | 10+2 or equivalent (2026 admission was based on JEE Main and CUET (UG) percentiles) |

---

## Features

- **Single-page home** with anchored sections: About, Programme, News and Events, Student Activities, Contacts.
- **Auto-advancing hero carousel** with four photographs, previous/next buttons, dot indicators, keyboard arrows, and pause on hover.
- **Horizontally scrolling card rows** for News and Events and for Student Activities, with scroll-snap and previous/next buttons that disable at the ends.
- **Light and dark theme** toggle, remembered across visits via `localStorage`.
- **Sticky navigation bar** with a *People* dropdown (Faculty, Students) and a mobile menu.
- **Graceful image fallbacks:** if an image file is missing, the `<img>` is removed and a striped placeholder background is shown instead.
- **Accessibility-minded markup:** skip link, ARIA labels and roles, visible focus outlines, 44px touch targets, and `prefers-reduced-motion` support.
- **No build step and no dependencies:** plain HTML, CSS and vanilla JavaScript.

---

## Repository Structure

```
isid-bsds.github.io/
├── index.html          # Home page (HTML + inline CSS + inline JS, ~440 lines)
├── README.md           # This file
├── assets/
│   └── images/         # Hero and section images (replaceable files)
└── people/
    ├── faculty.html    # Faculty page (linked from nav)
    └── students.html   # Students page (linked from nav)
```

**Image files referenced by `index.html`** (place them in `assets/images/`):

| File | Used for |
|---|---|
| `isi-delhi-campus.jpg` | Hero slide 1 (campus) |
| `bsds-batch.jpg` | Hero slide 2 (BSDS batch) |
| `academic-seminar.jpg` | Hero slide 3 (seminar or lecture) |
| `student-activities.jpg` | Hero slide 4 (student activities) |
| `mahalanobis.png` | Image in the "About ISI Delhi" section |

---

## Tech Stack

- **HTML5** (semantic landmarks: `header`, `nav`, `main`, `section`, `footer`, `address`, `time`)
- **CSS3** (custom properties for theming, CSS Grid, Flexbox, `clamp()` fluid sizing, scroll-snap, media queries)
- **Vanilla JavaScript** (carousel, tile scrolling, dropdown/mobile menu, theme toggle)
- **GitHub Pages** for hosting

Fonts are system stacks: Georgia / Times New Roman for headings, and the system UI sans-serif for body text. No external fonts or libraries are loaded.

---

## Getting Started

### Prerequisites

Just a web browser. Optionally, any static file server for local preview.

### Run locally

```bash
# 1. Clone the repository
git clone https://github.com/isid-bsds/isid-bsds.github.io.git
cd isid-bsds.github.io

# 2. Option A: open the file directly
open index.html          # macOS
xdg-open index.html      # Linux
start index.html         # Windows

# 2. Option B: serve it locally (recommended, so relative links behave like production)
python3 -m http.server 8000
# then visit http://localhost:8000
```

---

## Deployment (GitHub Pages)

The repository is named `isid-bsds.github.io`, so it is served as a **user/organisation site** at:

```
https://isid-bsds.github.io/
```

To deploy or redeploy:

1. Push your changes to the `main` branch.
2. In the repository, go to **Settings → Pages**.
3. Set the source to **Deploy from a branch**, branch `main`, folder `/ (root)`.
4. Wait a minute or two for the site to build, then refresh.

---

## Customising the Site

Everything on the home page lives in `index.html`.

### Hero images

Replace the files in `assets/images/` with your own photographs, keeping the same filenames (or update the `src` attributes in the `.hero` block). Recommended size is about **1600 × 700 px**. Each slide has descriptive `alt` text; update it when you change the photo.

### News and Events

Add a new `<li>` at the top of the `<ul class="news" id="news">` list:

```html
<li>
  <time datetime="2026-11-05">Nov 5, 2026</time>
  <div>
    <h3><a href="https://example.com/post">Event title</a></h3>
    <p>One or two sentences summarising the event.</p>
  </div>
</li>
```

### Student Activities

Add a new `<li>` inside `<ul class="news" id="act">`. The `tag` label (for example *Industry* or *Achievement*) appears as a small badge on the card:

```html
<li>
  <span class="tag">Achievement</span>
  <div>
    <h3>Title of the achievement</h3>
    <p>Short description.</p>
  </div>
</li>
```

### Contacts

Edit the `#contacts` section: postal address in the `<address>` block, and the programme coordinator's name, link, email and telephone in the `<dl>` list.

### Theme and colours

Colours are defined as CSS custom properties at the top of the `<style>` block.

```css
:root {
  --navy:#16284a;  --navy-2:#0f1d37;  --ink:#1d2330;  --muted:#5b6475;
  --line:#d9d6cd;  --paper:#fbfaf6;   --band:#f1eee6;
  --accent:#8c2f2f; --focus:#c28a00;
  --nav-h:64px;    --w:1120px;
}
```

Dark mode overrides the same variables under `html[data-theme="dark"]`. The user's choice is stored in `localStorage` under the key `theme` (`"light"` or `"dark"`), and a tiny inline script in `<head>` applies it before first paint to avoid a flash of the wrong theme.

### Carousel timing

Slides auto-advance every **2 seconds**. To change this, edit the `DELAY` constant in the inline script (value in milliseconds):

```js
var DELAY = 2000;
```

Auto-advance pauses while the pointer is over the hero, restarts after any manual click, and is disabled entirely for visitors who prefer reduced motion.

---

## Design and Accessibility Notes

- **Skip link** ("Skip to content") jumps to `<main id="main">`.
- **Keyboard support:** Left/Right arrows move through hero slides and scroll the news/activities rows; Escape closes the People dropdown.
- **ARIA:** the hero uses `role="region"` with `aria-roledescription="carousel"`; menu toggles expose `aria-expanded` and `aria-controls`; the current page is marked with `aria-current="page"`.
- **Touch targets:** buttons are at least 44 × 44 px.
- **Reduced motion:** smooth scrolling and slide transitions are turned off under `prefers-reduced-motion: reduce`.
- **Dark mode:** both themes keep text/background contrast through shared variables.

---

## Responsive Breakpoints

| Breakpoint | Behaviour |
|---|---|
| `≤ 1180px` | Navigation collapses into a "Menu" button; dropdown becomes an inline list |
| `≤ 900px` | Two-column layouts (About, Programme, Contacts, footer) stack into one column; hero text moves below the image overlay; pathway cards stack |
| `≤ 600px` | Smaller type and padding; news cards fill about 82% of the viewport width; carousel controls are centred |

---

## Contributing

Contributions that improve accuracy, accessibility or design are welcome.

1. Fork the repository.
2. Create a branch: `git checkout -b feature/short-description`
3. Make your changes and test locally (including the narrow mobile layout and dark mode).
4. Commit with a clear message: `git commit -m "Add Oct 2026 seminar to news"`
5. Push and open a pull request describing what changed and why.

**Content guidelines**

- Keep information factual and link to an official or primary source where possible.
- Do not publish personal contact details of students without their consent.
- Ensure every image has meaningful `alt` text and that you have permission to use it.

---

## Disclaimer

This is the **unofficial** website of the BSDS Programme run at the Indian Statistical Institute, Delhi Centre. It is a prototype maintained by students and is not affiliated with or endorsed by the Institute. Always verify admissions, curriculum and regulatory details on the [official ISI pages](https://www.isical.ac.in/).

&copy; 2026 Indian Statistical Institute
