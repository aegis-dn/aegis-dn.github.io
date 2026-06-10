# aegis-dn.github.io

Recruitment website for **AEGIS — Adaptive Grid-Interactive Edge Datacenter Fleets**, an EU Horizon Europe Marie Skłodowska-Curie Doctoral Network (grant agreement No 101311399) running 2026–2030.

The site's main job is to recruit the network's 15 Doctoral Candidates (PhD positions). It is a static [Jekyll](https://jekyllrb.com/) site served by GitHub Pages at https://aegis-dn.github.io.

## Structure

- `index.md`, `*.md` — content pages (Home, About, Research, Partners, Positions, Why join?, Requirements, How to apply, News)
- `positions/dc01.md` … `dc15.md` — one page per Doctoral Candidate position
- `_layouts/default.html` — the single page layout (logo header, nav, EU funding footer)
- `_includes/apply-block.html` — the shared "How to apply" block used on every position page; the central application-portal link lives **only** here, so it is a one-line change when the real URL is ready
- `assets/` — logo, EU flag, beneficiary logos, stylesheet

## Updating positions

- When a host institution publishes an official vacancy, edit that position's `positions/dcNN.md` and replace the "link coming soon" line.
- When the central application portal URL is ready, edit the single link in `_includes/apply-block.html`.
- Position status badges (`opening soon` / `open` / `filled`) are set in `positions.md`.

## Run locally

```sh
gem install bundler jekyll
jekyll serve
# open http://localhost:4000
```
