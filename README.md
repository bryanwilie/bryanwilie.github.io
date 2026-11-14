# bryanwilie.github.io

My personal page: <https://bryanwilie.github.io/>

It is a [Jekyll](https://jekyllrb.com/) site built on the [al-folio](https://github.com/alshedivat/al-folio) theme, with a small custom style layer on top. Everything you normally need to change is in the few files listed below. You can edit them directly on GitHub (pencil icon) and commit; the site redeploys by itself.

## Where to change what

| I want to change...                                              | Edit this                                                            |
| ---------------------------------------------------------------- | -------------------------------------------------------------------- |
| The home page text (bio, "open to roles" box, Service)           | [`_pages/about.md`](_pages/about.md)                                 |
| The line under my name (e.g. "NLP & ML Researcher · PhD, HKUST") | `subtitle:` at the top of [`_pages/about.md`](_pages/about.md)       |
| My profile photo                                                 | Add the image to `assets/img/`, then set `profile.image` in `_pages/about.md` |
| Contact icons (email, Scholar, GitHub, LinkedIn, X)              | [`_config.yml`](_config.yml), the "Social integration" section       |
| My email address                                                 | `email:` at the top of [`_config.yml`](_config.yml)                  |
| The page description (shown in search results and link previews) | `description:` at the top of [`_config.yml`](_config.yml)            |
| Publications                                                     | [`_bibliography/papers.bib`](_bibliography/papers.bib)               |
| The CV                                                           | `assets/pdf/cv.pdf` (see [Updating my CV](#updating-my-cv))          |
| Colors (light and dark mode)                                     | [`_sass/_themes.scss`](_sass/_themes.scss)                           |
| Fonts, spacing, button and section styling                       | [`_sass/_custom.scss`](_sass/_custom.scss)                           |
| Navigation bar tabs                                              | `nav:` / `nav_order:` at the top of each file in `_pages/`           |

### Home page (`_pages/about.md`)

- The part between the two `---` lines at the top is the page settings (subtitle, photo, which sections to show). Leave `social: true` so the contact icons and CV button stay at the bottom.
- Below it is plain Markdown. Edit the bio, the "open to roles" box (`<div class="callout">`), and the **Service** list (Area Chair / Reviewer) the same way you would edit any text.
- `{{ site.email | encode_email }}` in the callout is filled from `email:` in `_config.yml`; keep it as is.

### Contact icons (`_config.yml`)

Fill in or clear the username next to each key (`github_username`, `linkedin_username`, `x_username`, `scholar_userid`, ...). An icon appears only when its value is not empty, so leave a key blank to hide that icon.

### Publications (`_bibliography/papers.bib`)

The Publications tab is generated from this file and is **always sorted newest first** (by `year`, then `month`). Add a new paper by pasting an entry at the top (the position in the file does not matter):

```bibtex
@inproceedings{wilie2027example,
    abbr = {ICLR},
    title = {An Example Paper Title},
    author = {Wilie, Bryan and Coauthor, Alice and Coauthor, Bob},
    booktitle = {Proceedings of the 15th International Conference on Learning Representations},
    month = apr,
    year = {2027},
    paper = {https://openreview.net/forum?id=XXXX},
    code = {https://github.com/bryanwilie/example},
    abstract = {The abstract text. It shows up when you click the "Abs" button.},
}
```

- `title`, `author`, `booktitle`, `year` are required. Always add `month` (`jan`, `feb`, ..., `dec`); without it, the paper sorts last within its year.
- `paper` (link to the PDF or page) and `code` (link to the repo) are optional and add a **Paper** / **Code** button. `abstract` adds an **Abs** button.
- `abbr` is a short venue name. It is currently not displayed, but keep it for reference.
- Wrap capital letters that must stay capital in braces, e.g. `{J}-{T}o{RL}`.
- The citation key (`wilie2027example`) must be unique.
- The "Google Scholar" link at the top of the Publications page is in [`_pages/publications.md`](_pages/publications.md).

### Updating my CV

The **CV** button at the bottom of the home page (to the right of the contact icons) opens `assets/pdf/cv.pdf`.

1. Name your file exactly `cv.pdf`.
2. On GitHub, open the [`assets/pdf`](assets/pdf) folder, click **Add file → Upload files**, drag `cv.pdf` in, and commit to `master`. To update later, upload a new `cv.pdf` the same way; it replaces the old one.
3. Wait a minute or two for the site to redeploy. The same URL, <https://bryanwilie.github.io/assets/pdf/cv.pdf>, always serves the newest CV.

The button is **only shown when `assets/pdf/cv.pdf` exists**, so visitors never get a dead link. If you want a different filename or location, change `cv_file:` in [`_config.yml`](_config.yml).

## Deploying

Pushing or merging to `master` triggers the **Deploy site** workflow ([`.github/workflows/deploy.yml`](.github/workflows/deploy.yml)), which builds the site and publishes it to the `gh-pages` branch. It starts when a change touches the page content, publications, styles, assets or config. Check progress in the repo's **Actions** tab. To redeploy without changing anything, open **Actions → Deploy site → Run workflow**.

GitHub Pages must serve the `gh-pages` branch (Settings → Pages → Source: *Deploy from a branch*, branch `gh-pages`, folder `/ (root)`).

## Previewing changes locally (optional)

Editing on GitHub and checking the live site is enough for most changes. To preview on your machine:

```bash
# Option A: Docker (easiest)
docker compose up
# then open http://localhost:8080

# Option B: Ruby
bundle install
bundle exec jekyll serve
# then open http://localhost:4000
```

See [`INSTALL.md`](INSTALL.md) for details and troubleshooting. Profile images need ImageMagick installed for local builds (Docker already has it).

## Repository layout

```
_pages/            Pages: about.md (home), publications.md, repositories.md, 404.md
_bibliography/     papers.bib, the publication list
_config.yml        Site settings, contact icons, CV path, publication sorting
_data/             Small data files (venue badge colors, repositories, ...)
_sass/             Styles: _themes.scss (colors), _custom.scss (my tweaks)
_layouts/          Page templates (about.liquid renders the bottom icons + CV button)
assets/img/        Images (profile photo)
assets/pdf/        The CV (cv.pdf)
```

`CONTRIBUTING.md`, `CUSTOMIZE.md`, `FAQ.md` and `INSTALL.md` are the original al-folio theme docs, kept for reference.

## Credits

Theme: [al-folio](https://github.com/alshedivat/al-folio) by Maruan Al-Shedivat and contributors, licensed under MIT (see [`LICENSE`](LICENSE)).
