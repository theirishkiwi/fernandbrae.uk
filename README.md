# Harbour Hide Co. — Hugo site

A flat-file site: every page is a small text file with a few fields at the
top. Edit a file, save, `git push` — Cloudflare Pages rebuilds and
republishes automatically.

## Adding or editing a bag

Each bag is one file in `content/bags/`. Copy an existing one, e.g.:

```
content/bags/anstruther-tote.md
```

and change the fields:

```yaml
---
title: "The Anstruther Tote"
weight: 1              # controls display order, lowest first
price: "£145"
materials: "Waxed canvas body, oiled-leather straps"
description: "A wide, unlined tote..."
shape: "tote"           # one of: tote, satchel, clutch, crossbody
---
```

To add a fifth bag, duplicate one of these files under a new name (e.g.
`content/bags/new-bag.md`), give it a new `weight`, and pick whichever
`shape` looks closest — or ask for a new SVG shape to be added to
`layouts/partials/bag-art.html`.

To remove a bag, delete its file.

## Editing the About page

Everything on the About page is a field in `content/about.md` — the
`story` list (paragraphs) and the `steps` list (the "how it's made"
list). Add, remove, or edit lines in either list; no HTML involved.

## Editing the homepage intro

`content/_index.md` holds the hero heading and the "current run"
heading/subtext.

## Once you have real product photos

Right now each bag and the About page use a simple line-drawn SVG
placeholder instead of a photo. To use a real photo instead:

1. Drop the image in `static/images/`, e.g. `static/images/tote.jpg`.
2. In `layouts/index.html`, `layouts/bags/single.html`, and
   `layouts/bags/list.html`, replace the
   `{{ partial "bag-art.html" .Params.shape }}` line with:
   `<img src="{{ "images/tote.jpg" | relURL }}" alt="{{ .Title }}">`
   (or add an `image:` field to each bag's front matter and reference
   `.Params.image` instead, so each bag can point at its own file).

## Running it locally

Install Hugo (https://gohugo.io/installation/), then from this folder:

```
hugo server
```

and open the local URL it prints.

## Cloudflare Pages build settings

If you're setting this up fresh, or reconnecting the project:

- Framework preset: **Hugo** (Cloudflare fills in the rest below automatically)
- Build command: `hugo --minify`
- Build output directory: `public`
- Environment variable `HUGO_VERSION` set to `0.135.0` (or newer) —
  without this Cloudflare may use an old default Hugo version that
  doesn't understand some of the syntax here.

Push this whole folder to the GitHub repo already connected to your
Cloudflare Pages project (replacing the old single `index.html`), and
it will rebuild on its own.
