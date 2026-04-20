# Deployment Guide — GitHub Pages Portfolio

This document walks you through everything you need to publish and maintain
your videography portfolio on **GitHub Pages** — GitHub's free static-site
hosting service. No server required.

---

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Repository structure](#repository-structure)
3. [First-time deployment](#first-time-deployment)
4. [Making changes after launch](#making-changes-after-launch)
5. [Adding a new video](#adding-a-new-video)
6. [Customising the site](#customising-the-site)
7. [Custom domain (optional)](#custom-domain-optional)
8. [Troubleshooting](#troubleshooting)

---

## Prerequisites

| Tool | Why | Install |
|------|-----|---------|
| Git | Version control — tracks every change | <https://git-scm.com> |
| GitHub account | Hosts the code and serves the site | <https://github.com> |
| A text editor | Editing HTML/CSS | VS Code recommended (<https://code.visualstudio.com>) |

You do **not** need Node.js, a build step, or any local server — the site is
plain HTML and CSS.

---

## Repository structure

```
Joosty.github.io/
├── index.html        ← Landing page (edit the hero text & showreel here)
├── portfolio.html    ← Video grid (add new videos here)
├── about.html        ← Bio, skills, gear (personalise this page)
├── styles.css        ← All visual styling (colours, layout, typography)
└── DEPLOYMENT.md     ← This file
```

All pages share one stylesheet (`styles.css`) — so a colour change there
updates every page at once.

---

## First-time deployment

### 1 — Fork or create your repository

If you are starting from scratch:
1. Log in to [github.com](https://github.com).
2. Click **+** → **New repository**.
3. Name it **exactly** `<your-github-username>.github.io`
   (e.g. `joebloggs.github.io`).  
   ⚠️ The name must match your username — this is how GitHub Pages works.
4. Set it to **Public**.
5. Click **Create repository**.

If the repository already exists (e.g. this one), skip to step 2.

---

### 2 — Upload your files

**Option A — GitHub web interface (no Git required)**

1. Open your repository on github.com.
2. Click **Add file → Upload files**.
3. Drag all four files (`index.html`, `portfolio.html`, `about.html`,
   `styles.css`) into the upload area.
4. Scroll down, add a commit message like `Initial portfolio upload`, and
   click **Commit changes**.

**Option B — Git command line**

```bash
# Clone your repository (replace URL with yours)
git clone https://github.com/<username>/<username>.github.io.git
cd <username>.github.io

# Copy the four site files into this folder, then:
git add .
git commit -m "Initial portfolio upload"
git push origin main
```

---

### 3 — Enable GitHub Pages

1. In your repository, click **Settings** (top tab bar).
2. Scroll down to **Pages** in the left sidebar.
3. Under **Build and deployment → Source**, select **Deploy from a branch**.
4. Set the branch to **main** and the folder to **/ (root)**.
5. Click **Save**.

GitHub will now build and deploy your site. After ~60 seconds, a green
banner will appear with your live URL:

```
https://<username>.github.io
```

> 💡 **First deploy can take 1–5 minutes.** Subsequent updates are usually
> live within 30 seconds.

---

### 4 — Verify the deployment

Visit the URL above. You should see your landing page. If you see a 404, wait
another minute and refresh.

You can monitor the deployment status under:
**Actions** tab → **pages-build-and-deployment** workflow.

---

## Making changes after launch

Every time you push changes to the `main` branch, GitHub Pages automatically
rebuilds and republishes the site. No manual step needed.

**Via the GitHub web interface (easiest):**

1. Open the file you want to edit (e.g. `portfolio.html`).
2. Click the **pencil icon** (Edit this file).
3. Make your changes.
4. Scroll down → write a commit message → **Commit changes**.
5. The site updates within ~30 seconds.

**Via Git locally (recommended for larger edits):**

```bash
# 1. Pull the latest version
git pull origin main

# 2. Edit files in your text editor

# 3. Stage and commit
git add .
git commit -m "Describe what you changed"

# 4. Push — this triggers the deployment
git push origin main
```

---

## Adding a new video

Open `portfolio.html` in your editor. Find the comment:

```html
<!-- ADD MORE VIDEOS BELOW — paste the template block above -->
```

Copy the template block shown above that comment and paste it before that
comment. Then fill in:

| Field | What to put |
|-------|-------------|
| `data-category` | Filter category slug, e.g. `short-film`, `event` |
| `data-video-id` | YouTube video ID (11 characters from the video URL) |
| `img src` | Replace the video ID in the thumbnail URL |
| `img alt` | Short description of the thumbnail |
| `video-card__tag` | Display label for the category badge |
| `video-card__title` | Video title |
| `video-card__desc` | One or two sentence description |
| `video-card__meta` | Year and duration |

**Finding a YouTube video ID:**

```
https://www.youtube.com/watch?v=dQw4w9WgXcQ
                               ^^^^^^^^^^^^ this is the 11-character ID
```

**Thumbnail URLs are automatic — YouTube generates them:**

```
https://img.youtube.com/vi/<VIDEO_ID>/maxresdefault.jpg
```

> 💡 If `maxresdefault.jpg` returns a blank/black image (the video doesn't
> have a HD thumbnail), use `hqdefault.jpg` instead.

---

## Customising the site

### Change your name

Search-and-replace `Your Name` in all four files.

### Change the accent colour

Open `styles.css`. At the top, find:

```css
:root {
    --accent: #e8c97d;   /* warm gold */
}
```

Replace `#e8c97d` with any hex colour you like. The change propagates
everywhere instantly.

### Update the showreel on the landing page

In `index.html`, find the `<iframe>` inside `.hero-reel` and replace the
video ID in the `src` attribute.

### Add a photo on the About page

1. Create an `images/` folder in the repository.
2. Upload your portrait (recommended: JPEG, ~800×1100 px, under 300 KB).
3. In `about.html`, replace the placeholder `<div>` with:

```html
<img class="about-photo__img"
     src="images/portrait.jpg"
     alt="Your Name — videographer">
```

### Add a new filter category

1. In `portfolio.html`, add a button inside `.portfolio-filters`:

```html
<button class="filter-btn" data-filter="travel">Travel</button>
```

2. Set `data-category="travel"` on every card that belongs to that category.

---

## Custom domain (optional)

If you own a domain (e.g. `yourname.com`):

1. In your repository, create a file called `CNAME` (no extension) containing
   just your domain:

   ```
   yourname.com
   ```

2. At your domain registrar, add a **CNAME record**:

   | Type  | Host | Value |
   |-------|------|-------|
   | CNAME | www  | `<username>.github.io` |

   And an **A record** pointing to GitHub's IP addresses:

   ```
   185.199.108.153
   185.199.109.153
   185.199.110.153
   185.199.111.153
   ```

3. In **Settings → Pages**, set the custom domain and enable **Enforce HTTPS**.

DNS propagation can take up to 24 hours.

---

## Troubleshooting

| Problem | Fix |
|---------|-----|
| Site shows 404 | Check the repository is **Public** and Pages is enabled on the `main` branch |
| Changes not appearing | Wait 60 s then hard-refresh (`Ctrl+Shift+R` / `Cmd+Shift+R`) |
| Video thumbnails are black | Use `hqdefault.jpg` instead of `maxresdefault.jpg` |
| Video won't play in modal | Ensure the YouTube video is set to **Public** (not unlisted or private) |
| Filter buttons don't work | Check `data-filter` on the button matches `data-category` on the card exactly |
| Broken layout on mobile | Open browser DevTools → toggle device mode to diagnose |

---

*Site built with plain HTML & CSS — no frameworks, no build step.*  
*Hosted for free on GitHub Pages.*
