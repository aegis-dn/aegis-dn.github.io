# aegis-dn.github.io — maintainer's guide

Recruitment website for **AEGIS — Adaptive Grid-Interactive Edge Datacenter Fleets**, an EU Horizon Europe Marie Skłodowska-Curie Doctoral Network (grant agreement No 101311399), running 2026–2030. The site's job is to recruit the network's 15 Doctoral Candidates (PhD positions).

It is a static [Jekyll](https://jekyllrb.com/) site (no theme gem, no JavaScript, GitHub-Pages-safe). This README is the working reference for how it's hosted and built.

## Hosting

| What | Where |
|---|---|
| Repo | `github.com/aegis-dn/aegis-dn.github.io` (public) |
| Hosting | GitHub Pages, built by the **`pages build and deployment`** GitHub Action on every push to `main` |
| Public URL | **https://aegis-dn.eu** (custom domain, set in the `CNAME` file) |
| DNS | Apex `aegis-dn.eu` → GitHub A/AAAA records; HTTPS is enforced. `aegis-dn.github.io` 301-redirects to `aegis-dn.eu`. DNS + HTTPS are already configured. |

**Deploy = `git push origin main`.** The Action builds and publishes within a minute or two.

> **Known gotcha:** the deploy step occasionally fails with a transient `401 Requires authentication` ("Creating Pages deployment failed"). The Jekyll build itself is fine. Fix: re-run the failed workflow, or push an empty commit (`git commit --allow-empty -m "rebuild" && git push`). It then succeeds.
>
> Watch a deploy: `gh run list --repo aegis-dn/aegis-dn.github.io --limit 1` then `gh run view <id>`. (Note: the `gh` token may lack rights to *cancel/rerun* Actions on the `aegis-dn` org even though `git push` works — pushing an empty commit is the reliable nudge.)

## Build & preview locally

GitHub Pages builds with its own Ruby, but to preview locally use the Homebrew Ruby + a dedicated gem home (the system Ruby 2.6 is too old for Jekyll 4):

```sh
export PATH="/opt/homebrew/opt/ruby/bin:$PATH"
export GEM_HOME="$HOME/.gem-jekyll"
export PATH="$GEM_HOME/bin:$PATH"
# one-time: gem install jekyll bundler

cd ~/git/aegis-dn.github.io
jekyll build                                   # -> _site/
jekyll serve --no-watch --host 127.0.0.1 --port 4001   # preview
# stop: pkill -f "jekyll serve"
```

## Repository layout

```
_config.yml              # url, kramdown, site settings
CNAME                    # aegis-dn.eu
_layouts/default.html    # the ONE layout: logo header, nav, EU funding footer, favicon links
_includes/apply-block.html  # shared "How to apply" block (the apply URL lives ONLY here)
assets/
  css/style.css          # all styling (FORA-derived colors: red #b3122b, grey borders #e2e2e2)
  aegis-logo.png         # header wordmark
  favicon.svg + .ico/png + apple-touch-icon.png   # red power-button favicon (from the logo SVG)
  orcid.svg              # green ORCID iD icon used on researcher entries
  eu-flag.jpeg           # footer
  logos/<10>.png         # beneficiary logos
index.md about.md research.md dn-benefits.md job-requirements.md how-to-apply.md news.md
partners.md  partners/<dtu,epfl,tuw,tub,icl,lu,aalto,ericsson,dell,tdc>.md
positions.md positions/dc01.md … dc15.md
```

## Updating common things

- Edit Markdown pages directly.
- Change the apply link in the shared apply include.
- Update position status in the positions index and the relevant position page.
