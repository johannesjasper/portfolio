# Plain HTML Migration Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Replace Jekyll site with a single self-contained `index.html` + `style.css`, zero dependencies.

**Architecture:** Two-zone single-column page (personal identity → work), centered ~580px column, system fonts, inline SVG icons. No JS, no build step, no external resources.

**Tech Stack:** HTML5, CSS3 (no frameworks, no preprocessors)

---

### Task 1: Create `style.css`

**Files:**
- Create: `style.css`

**Step 1: Write the file**

```css
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

body {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', system-ui, sans-serif;
  font-size: 16px;
  line-height: 1.7;
  color: #333;
  background: #fff;
  padding: 4rem 1.5rem 3rem;
}

.wrapper {
  max-width: 560px;
  margin: 0 auto;
}

/* ── Header ── */
.header {
  text-align: center;
  margin-bottom: 3rem;
}

.avatar {
  width: 120px;
  height: 120px;
  border-radius: 50%;
  object-fit: cover;
  display: block;
  margin: 0 auto 1.2rem;
  filter: grayscale(20%);
}

.header h1 {
  font-size: 1.4rem;
  font-weight: 600;
  letter-spacing: -0.02em;
  color: #111;
  margin-bottom: 0.75rem;
}

.social {
  display: flex;
  justify-content: center;
  gap: 1rem;
}

.social a {
  color: #666;
  transition: color 0.15s;
}

.social a:hover {
  color: #111;
}

.social svg {
  display: block;
  width: 20px;
  height: 20px;
}

/* ── Zones ── */
.zone {
  margin-bottom: 2.5rem;
}

.zone p {
  text-align: justify;
  hyphens: auto;
  margin-bottom: 1em;
}

.zone p:last-child {
  margin-bottom: 0;
}

.divider {
  border: none;
  border-top: 1px solid #e8e8e8;
  margin: 2.5rem 0;
}

/* ── Links ── */
a {
  color: inherit;
  text-decoration: underline;
  text-decoration-color: #ccc;
  text-underline-offset: 2px;
  transition: text-decoration-color 0.15s;
}

a:hover {
  text-decoration-color: #333;
}

/* ── Footer ── */
footer {
  margin-top: 3rem;
  font-size: 0.8rem;
  color: #aaa;
  text-align: center;
}
```

**Step 2: Verify** — open in browser, check it loads without errors.

**Step 3: Commit**
```bash
git add style.css
git commit -m "add minimal CSS for plain HTML site"
```

---

### Task 2: Create `index.html`

**Files:**
- Create: `index.html`

**Step 1: Write the file**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Johannes Jasper · Software Engineer</title>
  <link rel="stylesheet" href="style.css">
  <link rel="icon" type="image/png" sizes="32x32" href="/public/favicons/favicon-32x32.png">
  <link rel="icon" type="image/png" sizes="16x16" href="/public/favicons/favicon-16x16.png">
  <link rel="apple-touch-icon" sizes="180x180" href="/public/favicons/apple-touch-icon.png">
  <link rel="shortcut icon" href="/public/favicons/favicon.ico">
  <meta name="description" content="Johannes Jasper — software engineer, coffee nerd, home brewer, and bike enthusiast based in Hamburg.">
</head>
<body>
  <div class="wrapper">

    <header class="header">
      <img class="avatar" src="/public/profile.png" alt="Johannes Jasper">
      <h1>Johannes Jasper</h1>
      <nav class="social" aria-label="Social links">
        <a href="https://github.com/johannesjasper" target="_blank" rel="noopener noreferrer" aria-label="GitHub">
          <!-- GitHub icon -->
          <svg viewBox="0 0 24 24" fill="currentColor" aria-hidden="true">
            <path d="M12 .297c-6.63 0-12 5.373-12 12 0 5.303 3.438 9.8 8.205 11.385.6.113.82-.258.82-.577 0-.285-.01-1.04-.015-2.04-3.338.724-4.042-1.61-4.042-1.61C4.422 18.07 3.633 17.7 3.633 17.7c-1.087-.744.084-.729.084-.729 1.205.084 1.838 1.236 1.838 1.236 1.07 1.835 2.809 1.305 3.495.998.108-.776.417-1.305.76-1.605-2.665-.3-5.466-1.332-5.466-5.93 0-1.31.465-2.38 1.235-3.22-.135-.303-.54-1.523.105-3.176 0 0 1.005-.322 3.3 1.23.96-.267 1.98-.399 3-.405 1.02.006 2.04.138 3 .405 2.28-1.552 3.285-1.23 3.285-1.23.645 1.653.24 2.873.12 3.176.765.84 1.23 1.91 1.23 3.22 0 4.61-2.805 5.625-5.475 5.92.42.36.81 1.096.81 2.22 0 1.606-.015 2.896-.015 3.286 0 .315.21.69.825.57C20.565 22.092 24 17.592 24 12.297c0-6.627-5.373-12-12-12"/>
          </svg>
        </a>
        <a href="https://www.linkedin.com/in/johannes-jasper" target="_blank" rel="noopener noreferrer" aria-label="LinkedIn">
          <!-- LinkedIn icon -->
          <svg viewBox="0 0 24 24" fill="currentColor" aria-hidden="true">
            <path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 01-2.063-2.065 2.064 2.064 0 112.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/>
          </svg>
        </a>
      </nav>
    </header>

    <main>
      <!-- Personal zone -->
      <section class="zone">
        <p>
          Hey, I'm Johannes — a coffee nerd, home brewer, bike enthusiast, and food lover
          based in Hamburg. I get unreasonably excited about a well-dialled espresso, a
          good ferment, and a long ride with too much elevation.
        </p>
      </section>

      <hr class="divider">

      <!-- Work zone -->
      <section class="zone">
        <p>
          I'm a software engineer with 10+ years building cloud-native systems. My focus is
          on the backend and infrastructure layers: event-driven microservices, distributed
          data pipelines, and the deployment machinery that keeps it all running.
        </p>
        <p>
          I work as an Agile Software Engineer at <a href="https://www.colenet.de" target="_blank" rel="noopener noreferrer">Colenet</a>,
          currently deployed to <a href="https://www.porsche.digital" target="_blank" rel="noopener noreferrer">Porsche Digital</a>
          where I'm part of the team building a serverless platform for global vehicle sales
          and contract management. Before that I worked on railway fleet management at
          <a href="https://www.vtg.com" target="_blank" rel="noopener noreferrer">VTG</a>,
          a freelance talent platform at
          <a href="https://www.workgenius.com" target="_blank" rel="noopener noreferrer">WorkGenius</a>,
          and spent several years at
          <a href="https://www.nexenio.com" target="_blank" rel="noopener noreferrer">neXenio</a>
          building Bdrive, an end-to-end encrypted file sharing solution for enterprise and
          government clients, where I grew from engineer to technical team lead.
        </p>
        <p>
          I'm also actively exploring how AI reshapes software development — building
          agentic tools and figuring out how to make these new capabilities actually useful.
        </p>
      </section>
    </main>

    <footer>
      <p>&copy; 2026 Johannes Jasper</p>
    </footer>

  </div>
</body>
</html>
```

**Step 2: Open in browser and verify** — both zones render, photo shows, links work visually.

**Step 3: Commit**
```bash
git add index.html
git commit -m "add plain HTML index page, two-zone layout"
```

---

### Task 3: Clean up Jekyll files

**Files to delete:**
- `Gemfile`
- `Gemfile.lock`
- `.ruby-version`
- `_config.yml`
- `atom.xml`
- `keybase.txt`
- `styles.scss`
- `vendor/` (whole dir)
- `_layouts/` (whole dir)
- `_includes/` (whole dir)
- `_sass/` (whole dir)
- `_bibliography/` (whole dir)
- `.jekyll-cache/` (whole dir)
- `404.html`
- `index.md`
- `content/` (CV drafts, no longer needed in repo)
- `license.txt`
- `.well-known/` (keybase verification)
- `docs/plans/` (this file — or keep it, up to preference)

**Step 1: Delete**
```bash
cd /Users/johannes/code/portfolio
rm -f Gemfile Gemfile.lock .ruby-version _config.yml atom.xml keybase.txt styles.scss 404.html index.md license.txt
rm -rf vendor _layouts _includes _sass _bibliography .jekyll-cache .well-known content
```

**Step 2: Verify** — `ls` shows only `index.html`, `style.css`, `public/`, `README.md`, `docs/`, `.gitignore`, `.claude/`

**Step 3: Update `.gitignore`** — remove Jekyll-specific entries, add any new ones.

**Step 4: Commit**
```bash
git add -A
git commit -m "remove Jekyll, clean up repository"
```

---

### Task 4: Write `README.md`

**Files:**
- Modify: `README.md` (rewrite completely)

**Step 1: Write the file**

```markdown
# johannesjasper.de

Personal website — plain HTML and CSS, no build step.

## Structure

```
index.html       — the page
style.css        — all styles
public/
  profile.png    — profile photo
  favicons/      — favicon set
```

## Development

Open `index.html` directly in a browser. No server required.

For live-reload during editing, any static server works:

```bash
# Python (no install needed)
python3 -m http.server 4000

# Or use any other static server
```

## Deployment

Copy `index.html`, `style.css`, and `public/` to the web server:

```bash
rsync -av --delete \
  index.html style.css public/ \
  user@host:~/www/www.johannesjasper.de/
```
```

**Step 2: Commit**
```bash
git add README.md
git commit -m "add README with setup and deploy instructions"
```
