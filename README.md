# Heterarchy Books

A curated library of books for [The Heterarchy Society](https://heterarchy.cz). Each book lives in its own directory; a build script compiles them into static JSON deployed via GitHub Pages.

- **Browse:** [heterarchy.fyi/books](https://heterarchy.fyi/books)
- **API / bundle:** [books.data.heterarchy.fyi](https://books.data.heterarchy.fyi/)

## Adding or editing books

Each book lives in `books/{id}/`. The directory name becomes the book's ID — use lowercase kebab-case (e.g. `sovereign-individual/`). Put metadata in `index.yaml` and the cover image in the same directory as `cover.jpg` (or `.png`, `.webp`, `.gif`).

**Fields:**

| Field | Required | Type | Description |
|-------|----------|------|-------------|
| `title` | yes | string | Full title of the book |
| `authors` | yes | string[] | Author(s); use `Name\|people-id` to link to a people profile |
| `description` | yes | string | Short description |
| `language` | yes | string[] | Language codes (`en`, `cs`, `de`) |
| `formats` | yes | string[] | Available formats (`ebook`, `pdf`, `web`, `print`) |
| `physical` | yes | boolean | Available as a physical copy in the library |
| `links` | yes | object[] | Links to read/buy (`href` + `label` required, `external` optional) |
| `cover` | no | string | Cover filename in the book directory (e.g. `cover.jpg`) |
| `year` | no | string | Publication year |
| `glossary` | no | string[] | Related glossary term IDs |
| `source` | no | object | Where the book was sourced from (`name` + `href`) |

**Example** (`books/sovereign-individual/index.yaml`):

```yaml
cover: cover.jpg
title: The Sovereign Individual
authors:
  - James Dale Davidson
  - William Rees-Mogg
year: "1997"
description: |
  Mastering the Transition to the Information Age.
language: [en]
formats: [ebook]
physical: false
glossary: [self-sovereignty, digital-autonomy]
links:
  - href: https://archive.org/details/the-sovereign-individual
    label: "→ číst na archive.org"
    external: true
source:
  name: Sovereign Engineering
  href: https://sovereignengineering.io/books
```

## Development

```bash
bun install
bun run build   # generate dist/ output
```

## Output

The build generates:
- `dist/index.json` — all books with metadata
- `dist/books.js` — ES module export
- `dist/books/{id}/` — cover images and resized variants
- `dist/history/{id}.json` — per-book commit history with diffs
- `dist/changelog.json` — all commits with referenced book changes

## Deployment

Pushing to `main` triggers GitHub Actions to build and deploy `dist/` to GitHub Pages. Enable Pages in your repository settings with source set to **GitHub Actions**.
