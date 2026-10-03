# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Personal academic homepage for Qixiang (Elliot) Zhang, built on the
[luost26/academic-homepage](https://github.com/luost26/academic-homepage) Jekyll template.
The template is **vendored** (`_layouts/`, `_includes/`, `_sass`-less CSS are all local
files), so edits are made directly rather than by overriding a remote theme.

Served at `https://elliot-qxzhang.github.io` from the `main` branch.

## Commands

```bash
bundle exec jekyll serve   # local preview
bundle exec jekyll build   # one-off build
```

There is no test suite, linter, or CI config. Verification means building and
inspecting the output.

## Deployment constraint: native GitHub Pages build

There is **no `.github/workflows/`** — GitHub Pages builds this repo with its own
Jekyll pipeline. Consequences that constrain every change:

- Only [whitelisted plugins](https://pages.github.com/versions/) load. Do not add
  gems (no `jekyll-polyglot`, no `jekyll-archives`, …). Switching to a custom
  Actions workflow would change the deployment model — confirm before proposing it.
- Keep `baseurl: ""`, and keep routing assets/links through `relative_url`.
- GitHub Pages runs Jekyll 3.10 with `jekyll-theme-primer` as the default theme;
  that theme is irrelevant because all layouts are local, and its appearance in the
  build log is not an error.
- The `jekyll-email-protect` plugin in `_config.yml` is NOT whitelisted, so
  `encode_email` is an unknown filter on Pages. Liquid is non-strict by default, so
  it passes the value through instead of failing — the email renders unobfuscated.

## Content lives in `_data/`, not in collections

Publications and news were migrated out of per-file collections into single YAML
files. `_config.yml` now declares only the `showcase` collection.

| File | Holds |
| --- | --- |
| `_data/publications.yml` | all publications (one list entry each) |
| `_data/news.yml` | all news entries |
| `_data/profile.yml` | bio, positions, education, experience, awards, contact links |
| `_data/professional_activities.yml` | journal/conference review service |
| `_data/misc.yml` | "Life Beyond AI" text |
| `_data/i18n.yml` | every UI string, in both languages |
| `_data/navigation.yml` | navbar entries |
| `_data/display.yml` | homepage section toggles, footer text |

Adding a publication or news item means appending one YAML entry — no new files,
no template edits.

`_data/authors.yml` still contains the template's placeholder authors
("Your Name", "Robert White", …). Real co-authors are not registered, so author
names render as plain text and the bold on "Qixiang Zhang" is hardcoded as `<b>`
inside each entry's `authors` list rather than using the template's `bold: true`
mechanism.

## Two traps in `_data` dates

Both of these broke the production build or the page order; do not reintroduce them.

**1. `UTC` suffixes silently become Strings.** Jekyll coerces front-matter `date`
into a `Time` (`jekyll/document.rb`, via `Utils.parse_date`), but `_data/*.yml` is
read with plain `SafeYAML.load_file` (`jekyll/readers/data_reader.rb`) with **no such
coercion**. ` UTC` is not a valid YAML timestamp timezone, so `2026-01-26 17:30:00 UTC`
parses as a String while neighbours parse as `Time`. `sort: "date"` then raises
`ArgumentError: comparison of String with Time failed` and the build fails.
Always write a numeric offset: `+0000`, `+0800`.

**2. Identical timestamps make order non-deterministic.** Jekyll's `sort_input`
compares only the extracted property, so ties do not crash — but Ruby's `sort!` is
not stable, so tied entries can swap. Six entries carry a deliberate `+1s` offset
(`...:01`) purely to pin the intended display order (only the year, or `%b %d`, is
ever shown). Give every new entry a unique timestamp.

Quick check:

```bash
ruby -ryaml -e 'd=YAML.load_file("_data/news.yml"); puts d.map{|e| e["date"].class}.tally; puts d.map{|x| x["date"]}.tally.select{|_,v| v>1}.inspect'
```

## Bilingual structure

English is the default and lives at the original URLs; Chinese mirrors it under `/zh/`.

- `index.html`, `publications.html` → `/`, `/publications`
- `zh/index.html`, `zh/publications.html` → `/zh/`, `/zh/publications`

Each page declares an explicit `permalink`. This is **load-bearing**: without it
`page.url` is `/publications.html`, and the navbar would derive a link to a
nonexistent `/zh/publications.html`. `_config.yml` `defaults` inject `lang: en`
site-wide and `lang: zh` under `zh/`.

Every template that renders text starts with:

```liquid
{%- assign lang = page.lang | default: 'en' -%}
{%- assign t = site.data.i18n[lang] -%}
```

Includes do not inherit variables, so this pair is repeated per file rather than set
once in the layout. The exceptions are `_includes/widgets/carousel.html` (used only
by `_showcase/` demo content) and `debug_repo_name.html` / `debug_url.html`, which
are orphaned — they were template setup warnings, removed from `index.html`.

Three conventions for reading data:

- UI strings: `{{ t.some_key }}`. **Every key must exist under both `en:` and `zh:`**
  in `_data/i18n.yml` — a missing key renders as an empty string, not an error.
- Translated content: `{{ field[lang] | default: field.en }}`. The `default` makes an
  untranslated field fall back to English.
- Shared content (dates, URLs, logos, emails, venue names, paper titles): read
  directly, stored once.

Deliberately kept in English on both versions: paper titles, author names, venue
names, and journal/conference names in `_data/professional_activities.yml` — they are
citable identifiers and proper nouns.

The language switcher is a `nav-item` at the end of the navbar `<ul>`, so it inherits
Bootstrap styling and mobile collapse. It derives the counterpart URL from
`page.url` by stripping or prepending `/zh`. A page with no translation sets
`translated: false` in its front matter (see `showcase.html`) and the switcher
falls back to that language's home page instead of linking to a 404.

Adding a page requires: a file at the root, a mirror under `zh/`, explicit
`permalink` on both, a `navbar_key` matching an entry in `_data/navigation.yml`, and
title strings where needed.

Navbar highlighting matches `item.key == page.navbar_key`, not the displayed label —
comparing labels breaks once they are localized.

## Styling

Bootstrap 4.6, Font Awesome, Academicons, and KaTeX all load from CDNs in
`_layouts/default.html`. The only local stylesheet is `assets/css/global.css`.

Scope new CSS tightly. In particular `.nav-link` is shared between the navbar and
the sticky year sidebar (`#navbar-year`) on the publications page, so styling it
globally affects both. The language switcher rules are namespaced under
`.lang-switcher` for this reason.

## Local verification without Jekyll

If `bundle`/`jekyll` cannot be installed (e.g. no `ruby-dev` for native extensions),
the pure-Ruby `liquid` gem plus Jekyll's own gem source can render templates
directly. Load the real `Jekyll::Filters` from the installed gem rather than
hand-writing stubs for `sort`/`where`/`date` — a stubbed `sort` that coerces dates to
`Time` hides exactly the String/Time bug described above and produces a false pass.
Only `relative_url`, `absolute_url`, and `encode_email` genuinely need local stubs,
since they require a live `Jekyll::Site`.

When changing templates or data, compare rendered output against the pre-change
commit (via `git worktree`) to confirm the English pages are unchanged and that
entry ordering still matches.
