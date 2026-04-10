# CLAUDE.md — AI Assistant Guide for josemorenoj.github.io

## Project Overview

This is a **static personal portfolio/CV website** for Jose Moreno, an Electromechanical Engineer turned Software Engineer. The site is hosted on **GitHub Pages** and is based on the [HTML5 UP "Read Only"](https://html5up.net/read-only) template.

There is **no build system, no package manager, and no server-side processing**. The site is a single `index.html` file with supporting assets, deployed directly from the repository root.

---

## Repository Structure

```
josemorenoj.github.io/
├── index.html              # Main presentation page (About, Skills, Contact)
├── portfolio.html          # Portfolio/accomplishments page
├── experience.html         # Work history and education page
├── README.md               # Template credits and attribution
├── LICENSE.txt             # Creative Commons Attribution 3.0
├── .gitignore              # Generic C/C++ gitignore (template artifact)
├── assets/
│   ├── css/
│   │   ├── main.css            # Compiled CSS (3,315 lines — DO NOT EDIT DIRECTLY)
│   │   └── fontawesome-all.min.css  # Font Awesome icons (minified)
│   ├── js/
│   │   ├── main.js             # Custom site behavior (scroll nav, panels)
│   │   ├── jquery.min.js       # jQuery core
│   │   ├── jquery.scrollex.min.js   # Scroll event detection plugin
│   │   ├── jquery.scrolly.min.js    # Smooth scroll anchor plugin
│   │   ├── browser.min.js      # Browser capability detection
│   │   ├── breakpoints.min.js  # Responsive breakpoints helper
│   │   └── util.js             # Utility functions and polyfills
│   ├── sass/
│   │   ├── main.scss           # Primary stylesheet source (1,828 lines)
│   │   └── libs/
│   │       ├── _vars.scss      # SASS variables (colors, fonts, sizes)
│   │       ├── _functions.scss # Helper functions
│   │       ├── _mixins.scss    # Reusable mixins
│   │       ├── _breakpoints.scss    # Responsive breakpoints definitions
│   │       ├── _html-grid.scss # Grid layout system
│   │       └── _vendor.scss    # Vendor prefix helpers
│   └── webfonts/               # Font Awesome icon font files (.ttf, .woff, .woff2, .svg, .eot)
└── images/
    ├── avatar.jpg              # Profile photo (sidebar)
    ├── banner.jpg              # Full-width hero banner
    ├── dashboard.jpg           # Accomplishments: Visteon project
    ├── metro.jpg               # Accomplishments: Siemens/Paris Metro project
    ├── space.jpg               # Accomplishments: EnduroSat/CubeSat project
    └── pic01.jpg, pic02.jpg, pic03.jpg  # Template placeholder images
```

---

## How the Site Is Built and Deployed

- **No build step required.** Files are served as-is by GitHub Pages from the repository root.
- The compiled `assets/css/main.css` is checked into the repository. It was generated from `assets/sass/main.scss` but there is no automated SASS compilation step.
- **Deployment:** Pushing to the `master` branch automatically deploys via GitHub Pages at `https://josemorenoj.github.io`.

---

## Multi-Page Structure

The site is split across three HTML files. Each file is self-contained and shares the same `<head>`, sidebar `#header`, and `<script>` blocks (duplicated — no templating engine available).

| File               | Sections                                              |
|--------------------|-------------------------------------------------------|
| `index.html`       | `#about`, `#things`, `#contact`, `#footer`            |
| `portfolio.html`   | `#banner`, `#accomplishments`, `#footer`              |
| `experience.html`  | `#banner`, `#history`, `#diplomas`, `#footer`         |

**Contact section** (`#contact`) lives only in `index.html`. Nav links on `portfolio.html` and `experience.html` point to `index.html#contact`.

### Navigation map

| Nav item   | `index.html`       | `portfolio.html`     | `experience.html`    |
|------------|--------------------|----------------------|----------------------|
| About      | `#about`           | `index.html`         | `index.html`         |
| Portfolio  | `portfolio.html`   | `#accomplishments`   | `portfolio.html`     |
| Experience | `experience.html`  | `experience.html`    | `#history`           |
| Education  | —                  | —                    | `#diplomas`          |
| Contact    | `#contact`         | `index.html#contact` | `index.html#contact` |

### Scroll-highlighting behaviour

`main.js` wires up `scrollex` only for nav links whose `href` starts with `#` and matches an element on the current page. Cross-page links (e.g. `portfolio.html`) are ignored by scrollex automatically — the browser handles them as normal navigations.

### Editing workflow

1. Open the relevant HTML file in an editor.
2. Locate the `<section id="...">` block to change.
3. Make content edits.
4. Test locally by opening the file in a browser (no server needed).
5. Commit and push to `master` to deploy.

### Keeping shared markup in sync

The `#header` sidebar (avatar, name, nav) and the `<head>` / `<script>` blocks are duplicated across all three files. If you update one (e.g. add a social link to the sidebar footer), apply the same change to all three files.

---

## Styling Conventions

- **SASS source** is in `assets/sass/main.scss` with partials in `assets/sass/libs/`.
- **Do NOT edit `assets/css/main.css` directly** — it is a compiled artifact.
- If you need to change styles, edit the `.scss` source and recompile. No build tool is configured; you will need to run SASS manually (e.g., `sass assets/sass/main.scss assets/css/main.css`).
- Responsive breakpoints are defined in `assets/sass/libs/_breakpoints.scss`: `xsmall`, `small`, `medium`, `large`, `xlarge`.
- Body font: **Lato** (Google Fonts). Monospace font: **Source Code Pro** (Google Fonts).
- Icons use **Font Awesome 5** classes (e.g., `fa-solid fa-code`).

---

## JavaScript Conventions

- All JavaScript is **jQuery-based**. No ES6 modules, no bundlers.
- `assets/js/main.js` contains all custom behavior:
  - Sidebar/panel toggle for mobile
  - Navigation link auto-highlighting on scroll (via `jquery.scrollex`)
  - Smooth scrolling for anchor links (via `jquery.scrolly`)
  - CSS `object-fit` polyfill for older browsers
- Do not introduce module syntax (`import`/`export`) — there is no bundler.
- Minified third-party libraries should not be modified.

---

## Images

- Profile photo: `images/avatar.jpg` (displayed in the `#header` sidebar)
- Hero banner: `images/banner.jpg` (full-width background image)
- Project thumbnails: `images/metro.jpg`, `images/dashboard.jpg`, `images/space.jpg`
- To add a new image, place it in the `images/` directory and reference it in `index.html`.

---

## Key Constraints

1. **Single-page site** — all content is in one `index.html`. There are no partials, templates, or CMS.
2. **No package.json, Gemfile, or build configuration** — do not try to run `npm install`, `bundle install`, or similar.
3. **No test suite** — visual inspection in a browser is the only testing method.
4. **No CI/CD pipeline** — deployment is triggered by pushing to `master`.
5. **Assets are pre-compiled/minified** — `main.css` and all `*.min.js` files should not be regenerated unless SASS is available.
6. **Template attribution required** — `README.md` credits HTML5 UP under the Creative Commons Attribution 3.0 license. Do not remove credits.

---

## Git Workflow

- Default deployment branch: `master`
- Feature branches are merged into `master` via pull requests (see commit history: `reface-website` → `master`).
- Branch naming convention observed: `reface-website`, `claude/add-claude-documentation-y1v2z`.

---

## Personal Information in the Site

The site contains real personal contact details. Be careful when:
- Logging or echoing file contents that may expose personal data (email address).
- Committing any changes that could inadvertently modify or remove contact information.

Current contact details (email, LinkedIn, GitHub) are in the `#contact` section of `index.html`.

---

## Common Tasks

### Update work experience
Edit the `<section id="history">` block in `experience.html`. Each job entry follows this pattern:
```html
<div class="col-4 col-12-small">
  <h3>Job Title @ Company</h3>
  <p>Date range | Location | Technologies used</p>
</div>
```

### Add a new accomplishment/project
Edit the `<section id="accomplishments">` block in `portfolio.html`. Use the existing `<article>` elements as a template. Note: the `<a class="image">` wrapper has no `href` by design — there are no detail anchor pages.
```html
<article>
  <a href="#" class="image"><img src="images/your-image.jpg" alt="" /></a>
  <div class="inner">
    <h4>Project Title</h4>
    <p>Project description...</p>
  </div>
</article>
```

### Update education/certifications
Edit the `<section id="diplomas">` block in `experience.html`. Follow the existing entry format.

### Change profile photo
Replace `images/avatar.jpg` (keep the same filename) or update the `src` attribute in the `#header` section:
```html
<span class="image avatar"><img src="images/avatar.jpg" alt="" /></span>
```

### Change styles without SASS
If SASS is unavailable, make targeted edits directly in `assets/css/main.css`, clearly commenting any manual overrides so they can be reconciled with the SASS source later.
