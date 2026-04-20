# Videography Portfolio — GitHub Pages Site

A minimal, fully static videography portfolio built with plain HTML and CSS. No frameworks, no build step — just upload and go.

**Live site:** `https://<your-github-username>.github.io`

---

## Pages

| File | Description |
|------|-------------|
| `index.html` | Landing page — hero section, featured showreel, and quick stats |
| `portfolio.html` | Filterable video grid — add new videos here |
| `about.html` | Bio, skills, gear list, and contact links |
| `styles.css` | All styling for every page (single file) |
| `DEPLOYMENT.md` | Step-by-step guide for publishing and updating the site |

---

## Quick Start

1. **Fork or create** a GitHub repository named `<your-username>.github.io`.
2. **Upload** `index.html`, `portfolio.html`, `about.html`, and `styles.css`.
3. **Enable GitHub Pages** — go to *Settings → Pages → Deploy from branch → main / root*.
4. Your site will be live at `https://<your-username>.github.io` within a few minutes.

See [DEPLOYMENT.md](DEPLOYMENT.md) for the full walkthrough, including how to add videos, customise colours, and set up a custom domain.

---

## Personalisation Checklist

- [ ] Replace every instance of `Your Name` with your real name (across all four files).
- [ ] Update the showreel `<iframe>` in `index.html` with your YouTube video ID.
- [ ] Add your video cards to `portfolio.html`.
- [ ] Fill in your bio on `about.html` and add a portrait photo.
- [ ] Update social links (YouTube, Instagram) in the footer of each page.
- [ ] Change the accent colour in `styles.css` (CSS variable `--accent`).

---

## Accent Colour

Open `styles.css` and change the single variable at the top:

```css
:root {
    --accent: #e8c97d;  /* swap this hex value for any colour you like */
}
```

The change propagates instantly to every page.

---

## Adding a Video

In `portfolio.html`, copy the existing video card template and fill in:

- `data-category` — filter slug (e.g. `short-film`, `event`, `commercial`)
- `data-video-id` — 11-character YouTube ID from `youtube.com/watch?v=XXXXXXXXXXX`
- `img src` — thumbnail URL (`https://img.youtube.com/vi/<VIDEO_ID>/maxresdefault.jpg`)
- Title, description, and meta fields

---

## Tech Stack

- Pure HTML5 & CSS3 — no JavaScript frameworks
- Google Fonts (Inter)
- YouTube embed API for video playback
- Hosted on [GitHub Pages](https://pages.github.com/) (free)
