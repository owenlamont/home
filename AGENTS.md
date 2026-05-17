# Coding Agent Instructions

Guidance on how to navigate and modify this repository.

## What This Repo Is

This is the source for Owen Lamont's personal site and blog, published to
GitHub Pages at <https://owenlamont.github.io/home/>. It is a
[MkDocs](https://www.mkdocs.org/) project using the
[Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) theme,
with the `blog`, `rss`, `tags`, and `social` plugins enabled.

There is no application code here — content lives under `docs/` as Markdown,
and `mkdocs.yml` configures the site.

## Project Structure

- **/docs/** – Markdown source. `docs/index.md` is the landing page;
  `docs/blog/posts/` holds blog posts.
- **/docs/img/** – Images referenced by posts and the landing page.
- **/overrides/** – Material for MkDocs theme overrides (Jinja partials).
- **mkdocs.yml** – Site configuration (theme, plugins, social links).
- **prek.toml** – prek (pre-commit) linter configuration.
- **.rumdl.toml** – Markdown linter configuration.
- **.ryl.toml** – YAML linter configuration.
- **typos.toml** – Typos configuration.

## Workflow

- Work happens directly on `main`. There is no feature-branch convention for
  this repo; small, focused commits to `main` are the norm.
- Publishing is manual via `mkdocs gh-deploy`, which builds the site and
  force-pushes to the `gh-pages` branch. GitHub Pages serves from `gh-pages`.
  Do not run `mkdocs gh-deploy` without explicit approval — it writes to the
  remote.
- Never commit or push without explicit approval for that specific
  commit/push action. Approval is case-by-case and does not carry forward.

## Code Change Requirements

- After any edit, ensure all linters pass: `prek run --all-files`.
- Let prek auto-correct formatting issues where possible. If prek reports
  changes, rerun it to confirm a clean pass before fixing anything manually.
- Stage any new files before running prek so they are included in the
  checks.
- For non-trivial content changes, preview locally with `mkdocs serve`
  before considering the change complete.

## Writing Style

- Posts target a developer audience. Match the tone of existing posts under
  `docs/blog/posts/` — first-person, conversational, technical without being
  dry.
- Wrap Markdown at 88 columns (enforced by rumdl `MD013`). Code blocks and
  tables are exempt.
- Use unordered list markers as `-` (rumdl `MD004`).
- Horizontal rules use `---` (rumdl `MD035`).
- Blog post filenames are lowercase with underscores; place new posts under
  `docs/blog/posts/` with a `date:` front-matter field so the blog plugin
  orders them correctly.

## Tools

- `prek` runs the full hook suite locally; install once as a uv tool
  (`uv tool install prek`). The other linters (`rumdl`, `typos`, `ryl`) are
  invoked by prek and do not need separate installation.
- `mkdocs` and the Material theme are not pinned in this repo (no
  `pyproject.toml`); install them in a uv-managed environment when building
  locally:

  ```bash
  uv tool install mkdocs --with mkdocs-material --with mkdocs-rss-plugin
  ```

## What Not To Do

- Don't introduce Python source, `pyproject.toml`, or any package scaffolding
  — this repo is documentation only.
- Don't add files under `docs/` that aren't referenced from `mkdocs.yml`
  navigation or discovered automatically by the blog plugin, unless you also
  update the nav.
- Don't edit files under `site/` — that directory is the build output and is
  gitignored.
