# ASTRO HPC docs

Source for the group's documentation site, built with [MkDocs Material](https://squidfunk.github.io/mkdocs-material/) and published to GitHub Pages by the workflow in `.github/workflows/docs.yml` on every push to `main`.

## Editing

Pages are Markdown files in `docs/`. The sidebar order is set by `nav:` in `mkdocs.yml`.

- **Small fix:** open the file on GitHub, click the pencil icon, edit, commit. The site rebuilds in a minute or two.
- **New page:** add `docs/<name>.md` and list it under `nav:` in `mkdocs.yml`.

## Preview locally

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
mkdocs serve          # open http://127.0.0.1:8000
```

Before pushing bigger changes, `mkdocs build --strict` catches broken links.
