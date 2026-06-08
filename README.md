# Hetzner Portal Page — Translated HTMLs

This folder contains the Hetzner portal subpage, exported from Axure RP and
translated into **5 languages**. It is intended as a **content + visual
reference for the implementation in Hugo** (or any other CMS).

## What's in this folder

| File pattern | Purpose |
|---|---|
| `portals_darkmode_hetzner_<lang>.html`  | Dark-theme variant per language |
| `portals_lightmode_hetzner_<lang>.html` | Light-theme variant per language |
| `content-translations.csv`              | All translatable strings as a flat CSV (drop straight into Hugo i18n) |
| `assets/`                               | Cleanly-named WebP image assets |
| `data/` `files/` `images/` `resources/` | Axure assets (shared by all variants) |

## Languages

| Code | Language | Excel sheet (source of truth) |
|---|---|---|
| `en` | English | `Hetzner EN` |
| `de` | German  | `Hetzner DE` |
| `fr` | French  | `Hetzner FR` |
| `es` | Spanish | `Hetzner ES` |
| `nl` | Dutch   | `Hetzner NL` |

The **CSV is the source of truth**. The HTMLs are visual previews that show
what each translated string looks like in the original Axure layout.

## How to open the HTMLs

**Double-click any HTML file.** The bundled JS shim forces Axure to use its
default 1680px view, so the page renders even when the browser window is
narrower (without it, Axure picks an empty iPhone view and shows a black
screen on macOS Sequoia).

## Image assets

The visible content images (persona stockphotos, Desktop App mockup,
integration logos) have been swapped to cleanly-named WebPs in `assets/`.
Naming convention:

```
{lang}_getmyinvoices_{section}_{name}.webp

examples:
  en_getmyinvoices_industries_it-and-software.webp
  de_getmyinvoices_desktop-app_dark.webp
  en_getmyinvoices_integrations_datev.webp
```

Decorative Axure-generated SVGs (arrows, divider lines, step number circles)
are kept under `images/portals_*_hetzner/u123.svg` since they have no
production-asset equivalent.

## Brand-blue highlighting in headings

The page headings use the GetMyInvoices brand-blue (`#44A4DC`) on specific
keywords. The colouring rules (same across all languages, applied
semantically):

| Heading | Blue keyword(s) |
|---|---|
| Hero H1 | "Hetzner invoices" (or equivalent in language) |
| Social proof | "20,000 companies" (or equivalent) |
| What GMI does for Hetzner | GetMyInvoices, Hetzner |
| About Hetzner | Hetzner |
| Who uses GMI with Hetzner | Hetzner |
| How does it work? | "work?" portion |
| Proven performance by GMI | GetMyInvoices |
| Desktop App: ... | "Desktop App" portion |
| Frequently combined with | "combined with" portion |
| FAQ about Hetzner and GMI | Hetzner, GetMyInvoices |
| Ready to automate... | "Hetzner invoices?" (dark text on the blue CTA banner) |

## Hugo i18n workflow

Open `content-translations.csv` — each row is one translatable string:

```csv
section,element,occurrence,en,de,fr,es,nl
Hero,H1 (headline),1,Download your Hetzner invoices automatically,Hetzner-Rechnungen automatisch herunterladen,...
Hero,Subline,1,With GetMyInvoices you download...,Mit GetMyInvoices holen Sie sich...,...
```

Group by `section` to build per-section i18n keys.

## Regenerating

If Excel or the Axure HTML is updated, regenerate everything with:

```bash
python3 ../translate_hetzner.py
```
