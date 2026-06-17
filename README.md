# aegis-dn.github.io - maintainer guide

Recruitment website for **AEGIS - Adaptive Grid-Interactive Edge Datacenter Fleets**, an EU Horizon Europe Marie Sklodowska-Curie Doctoral Network (grant agreement No 101311399), running 2026-2030. The site's job is to recruit the network's 15 Doctoral Candidates (PhD positions).

It is a static [Jekyll](https://jekyllrb.com/) site: no theme gem, no JavaScript, and safe for GitHub Pages. Website pages are edited directly as Markdown.

## Hosting

| What | Where |
|---|---|
| Repo | `github.com/aegis-dn/aegis-dn.github.io` |
| Hosting | GitHub Pages, built by the **`pages build and deployment`** GitHub Action on every push to `main` |
| Public URL | **https://aegis-dn.eu** |
| Custom domain | Set in `CNAME` |

Deploying is just:

```sh
git push origin main
```

The GitHub Pages Action normally builds and publishes within a minute or two. If the deploy step fails while the Jekyll build itself succeeds, rerun the failed workflow from GitHub Actions or push an empty rebuild commit:

```sh
git commit --allow-empty -m "rebuild"
git push
```

## Editing Content

Edit the relevant `.md` file directly. The main page files live at the repository root, partner pages live under `partners/`, and position pages live under `positions/`.

Common files:

```text
index.md
about.md
research.md
partners.md
partners/<partner>.md
positions.md
positions/dc01.md ... positions/dc15.md
dn-benefits.md
job-requirements.md
how-to-apply.md
news.md
```

Use plain Markdown and keep changes focused. Do not edit `_site/`; it is build output.

## Local Preview

GitHub Pages builds with its own Ruby environment. For local preview on macOS, use Homebrew Ruby and a dedicated gem home:

```sh
export PATH="/opt/homebrew/opt/ruby/bin:$PATH"
export GEM_HOME="$HOME/.gem-jekyll"
export PATH="$GEM_HOME/bin:$PATH"
# one-time: gem install jekyll bundler

cd ~/git/aegis-dn.github.io
jekyll build
jekyll serve --no-watch --host 127.0.0.1 --port 4001
```

Then open `http://127.0.0.1:4001`.

## Repository Layout

```text
_config.yml              # site title, URL, Markdown engine, Jekyll excludes
CNAME                    # aegis-dn.eu
_layouts/default.html    # shared page layout, header, nav, footer, favicon links
_includes/apply-block.html  # shared "How to apply" block
assets/
  css/style.css          # site styling
  aegis-logo.png         # header wordmark
  favicon.*              # favicon and touch icons
  orcid.svg              # ORCID icon used on researcher entries
  eu-flag.jpeg           # footer
  logos/<partner>.png    # beneficiary logos
partners/                # one Markdown page per beneficiary
positions/               # one Markdown page per Doctoral Candidate position
```

## Common Updates

- **Apply link:** edit `_includes/apply-block.html`.
- **Position status:** edit `positions.md` and the relevant `positions/dcNN.md` page.
- **Official vacancy links:** edit the relevant `positions/dcNN.md` page.
- **Partner details or researchers:** edit the relevant `partners/<partner>.md` page.
- **ORCID links:** keep using the green `assets/orcid.svg` icon style already present in the pages.
- **Layout or visual styling:** edit `_layouts/default.html` or `assets/css/style.css`.

## Contributions

See [CONTRIBUTING.md](CONTRIBUTING.md) for the preferred workflows for PhD students, regular contributors, occasional contributors, email edits, and pull requests.
