# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Personal website of Elisa Bortolas (astrophysicist, INAF-Osservatorio Astronomico di Padova), served by GitHub Pages from the `main` branch at `ebortolas.github.io`. It's a static, single-page site built on the **"Read Only" template by HTML5 UP** (CCA 3.0 license: keep the HTML5 UP credit in the footer).

No package manager, linter or tests. GitHub Pages builds the site with Jekyll, and pushing to `main` publishes it. `index.html` has front matter (`layout: null`) and uses Liquid includes, so `python3 -m http.server` would show the raw `{% include %}` tags. To preview, run `export GEM_HOME="$HOME/gems" PATH="$HOME/gems/bin:$PATH"; jekyll serve` (Jekyll 4 and the `jekyll-theme-minimal` gem are installed in `~/gems`) and open http://localhost:4000. Google Chrome is installed, so `google-chrome --headless=new --screenshot=out.png --window-size=1440,2400 http://localhost:4000/` works for visual checks (use `--window-size=390,3000` for mobile).

## Structure

- `_includes/about.md` and `_includes/bio.md` hold the prose of the About (`#one`) and Bio (`#two`) sections as Markdown. `index.html` pulls them in with `{% capture x %}{% include x.md %}{% endcapture %}{{ x | markdownify }}`. Edit the text there, not in the HTML. To make another section editable the same way, follow this pattern. Each file has a short visible part followed by a collapsible `<details markdown="1"><summary>Read more</summary> … </details>` block (`markdown="1"` makes kramdown parse the Markdown inside; leave blank lines around the inner content and don't indent it). The "Read more" style is the `/* Details (Read more) */` block in `main.scss`/`main.css`.
- `_includes/cv.md` feeds the "CV and publications" section (`#cv`, between Bio and Research). It's a `ul.feature-icons` list (template style: Font Awesome icon in a teal circle). The CV item appears only if `files/CV_Bortolas.pdf` exists (Liquid check on `site.static_files`).
- `index.html` holds the page layout and the rest of the content. The fixed left sidebar (`#header`) has the avatar, name and nav. The scrolling main column (`#main`) has sections `#one` … `#five`, and each nav link points to a section id. `assets/js/main.js` uses scrollex to highlight the active nav link while scrolling, so a new section needs both a `<section id="...">` and a matching `<li><a href="#...">` in `#nav`.
- `assets/css/main.css` is the stylesheet the page loads. It's compiled from `assets/sass/main.scss` (plus `assets/sass/libs/`), but the repo has no Sass toolchain. If you edit the SCSS, recompile it yourself with `npx sass@1.69.5 --no-source-map assets/sass/main.scss assets/css/main.css` (newer sass needs a newer Node than the installed v18). Note that the full recompile reformats the whole file, so for small changes it's simpler to edit both the SCSS and `main.css` by hand.
- `assets/js/*` and `assets/webfonts/*` are vendored template files (jQuery, scrollex, scrolly, breakpoints, Font Awesome). Don't modify them.
- `images/` contains `avatar.jpg` (sidebar), `banner.jpg` (top of `#one`) and `pic01–03.jpg` (the `#three` feature cards). The page refers to these filenames directly, so if you replace an image, keep its name or update the `src` in `index.html`.
- GitHub Pages builds with Jekyll 3.10 plus the `github-pages` plugins, unlike the local Jekyll 4. One difference matters: `jekyll-optional-front-matter` renders **every** `.md` file in the repo as a page, so a file with Liquid-looking text (`{{`, `{%`) breaks the whole build. Files that aren't part of the site go in `exclude:` in `_config.yml` (this file is excluded for that reason). `_includes/` is safe.
- `_config.yml` is a leftover GitHub Pages theme config with default values (`jekyll-theme-minimal`, "Octocat's homepage") plus the `exclude:` list. `layout: null` in `index.html` keeps that theme from wrapping the page.
- `README.txt` is the original HTML5 UP template readme.

## Current state of the content

- Real content: the sidebar, `#one` (About) and `#two` (Bio), whose text lives in `_includes/`.
- `#four` ("Contact Me", nav label "More") shows email, postal address and phone from `_includes/contact.md`. The template's contact form was removed.
- Still template placeholder text (lorem ipsum, demo titles): `#three` ("A Few Accomplishments", nav label "Research").
- `#five` (the template's "Elements" demo of every styled component) is commented out, but the nav still links to `#five` as "Contact". The commented-out block is a useful reference for the template's available CSS classes (buttons, tables, grids, image styles).
- Sidebar footer icons link to GitHub (github.com/ebortolas) and ORCID. The page footer still says "© Untitled".
