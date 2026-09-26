# aadeshvarude.github.io

Personal portfolio for **Aadesh Surendra Varude** — Perception & Computer Vision Engineer.

Live at <https://aadeshvarude.github.io/>

## Structure

Static single-page site. No build step, no dependencies, no framework.

```
index.html                  # entire site: markup + inline CSS + inline JS
assets/
  Aadesh_Varude_Resume.pdf  # linked from nav, hero and footer
  ReQuBiS_CASE2021.pdf      # IEEE CASE 2021 paper
  avatar.jpg                # 640x640 portrait
  favicon-32.png, icon-512.png
  projects/                 # per-project videos, screenshots and reports
    thumb/                  # 640x360 project-card thumbnails
robots.txt, sitemap.xml, .nojekyll
```

## Sections

Hero (with Research Interests card) → impact metrics → expertise → experience
→ projects → publications → skills → education & coursework → contact.

## Projects

Each project card opens a modal with the full write-up, demo videos, result
screenshots, tags and links. All project content lives in one place — the
`<script type="application/json" id="projData">` block near the bottom of
`index.html`. To add or edit a project:

1. Add an entry to that JSON object, keyed by slug:
   ```jsonc
   "my-project": {
     "title": "...", "kind": "Planning", "meta": "Course · Institution",
     "desc": ["paragraph one", "paragraph two"],
     "media": [
       {"t":"video",   "src":"/assets/projects/x.mp4", "loop":true, "cap":"..."},
       {"t":"youtube", "id":"VIDEOID", "cap":"..."},
       {"t":"shot",    "src":"/assets/projects/y.jpg", "cap":"..."}
     ],
     "tags": ["..."],
     "links": [{"l":"Code","u":"https://...","i":"gh"}]   // i: gh | pdf | link
   }
   ```
2. Add a matching `<article class="proj rv" data-cat="vision">` card in the
   grid, with `<button class="pbtn" data-proj="my-project">`.
3. Drop a 640×360 thumbnail at `assets/projects/thumb/my-project.jpg`.
4. In the card footer, put the repo link and the "View details" label inside
   `<span class="pacts">` so they stay grouped and right-aligned:
   ```html
   <span class="pacts">
     <a class="ext" href="https://github.com/..." target="_blank" rel="noopener"
        title="View source on GitHub" aria-label="View source for X on GitHub">…</a>
     <span class="more">View details …</span>
   </span>
   ```
   The card title is a stretched link covering the whole card, so `a.ext` needs
   `position:relative; z-index:2` (already in its class) to stay clickable.

`data-cat` drives the filter bar; values: `vision`, `slam`, `dl`, `planning`,
`robotics` (space-separated for multiple). Keep the `All` count in the filter
bar in sync.

Videos with `"loop": true` autoplay muted and silent; omit it for clips with
audio so they get normal playback controls.

## Media conventions

Source footage is compressed before committing — browsers cannot play `.avi`,
and large files make the page crawl. Videos are H.264 MP4 with `+faststart`,
capped at 960px wide. Animated GIFs are converted to MP4 (roughly 10× smaller).
Screenshots are progressive JPEG, max 1400px wide.

## Editing

Colours are CSS custom properties in `:root` at the top of the `<style>` block.
The dark palette is defined twice — under `prefers-color-scheme: dark` and under
`[data-theme="dark"]` — so the manual toggle wins in both directions. Change both.

To update the résumé, replace `assets/Aadesh_Varude_Resume.pdf` (keep the filename).

## Deploy

Push to `main`. GitHub Pages serves it directly.
