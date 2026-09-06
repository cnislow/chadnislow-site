# Content fragments

Each planet's long-form content lives in `content/<planet-id>.html` — a plain HTML
*fragment* (no `<html>`, `<head>`, or `<body>` wrapper) that gets fetched and dropped
into the full-screen reading overlay.

## Rules

- One `<section id="slug">` per heading, where `slug` matches the `slug` field on that
  planet's `children` entry in `index.html`. That id is what the reader scrolls to and
  what the sticky nav highlights.
- No inline `<script>` — fragments are injected with `innerHTML`, so scripts inside them
  won't run.
- Relative links/images resolve against `index.html`'s location (e.g. `assets/photo.jpg`),
  not against the `content/` folder.

## Available components

- `<ol class="timeline">` — a career-timeline-style list. Each `<li>` is a
  `.when` / `.what` pair:

  ```html
  <li>
    <div class="when">2022 — Present</div>
    <div class="what">
      <h3>Role <span class="org">Company</span></h3>
      <p>What the work was.</p>
    </div>
  </li>
  ```

- `<ul class="pills">` — a row of rounded chips, e.g. for a skills list:

  ```html
  <ul class="pills"><li>Java</li><li>Python</li></ul>
  ```

Plain `<h2>`, `<h3>`, `<p>`, `<ul>`, `<a>`, and `<img>` are all styled already — just write
normal HTML for anything that isn't a timeline or a pill list.

## Per-heading files (not built yet, but supported)

Drop a file at `content/<planet-id>/<slug>.html` and it's used instead of that heading's
slice of `content/<planet-id>.html` — no code changes required. Until then, everything
comes from the one whole-planet file.

## Link-only headings

A child in `index.html` can carry an `href` instead of relying on a `<section>` — e.g. the
"Résumé ↓" entry under Professional opens `assets/resume.pdf` directly rather than the
overlay. Those headings don't need a matching `<section>` in the fragment file.
