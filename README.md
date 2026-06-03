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

Just **double-click any HTML file**. They include a small JS shim that prevents
the Axure runtime from falling back to its (empty) iPhone view on browser
windows narrower than 1680px (which would otherwise render as a black page on
macOS Sequoia and similar setups).

## How to extract strings for Hugo i18n

Open `content-translations.csv`. Each row maps to one translatable string:

```csv
section,element,occurrence,en,de,fr,es,nl
Hero,H1 (headline),1,Download your Hetzner invoices automatically,Hetzner Rechnungen automatisch herunterladen,...
Hero,Subline,1,With GetMyInvoices you download...,Mit GetMyInvoices laden Sie...,...
```

Group by `section` to build per-section i18n keys, e.g.

```yaml
# data/i18n/en.yaml
hero:
  h1: "Download your Hetzner invoices automatically"
  subline: "With GetMyInvoices you download…"
  cta: "Start for free"
```

## What is NOT translated (intentional)

The Axure export contains a handful of strings that are **not in the
translation Excel** and therefore remain in their original form:

- Sticky-note text inside the Axure design (yellow notes for designers/devs).
- The page navigation menu placeholders ("Menue").
- The footer placeholder text ("Lorem ipsum…", "Placeholder").

These are not part of the portal page content — the live Hugo footer + nav
should be reused as-is.

## Image alt texts

The Excel includes a separate sheet, `Image alt texts`, with per-image alt
text in all five languages. They are not embedded in this HTML output (the
HTMLs use the original Axure-generated SVG-IDs as alt). Use the sheet directly
when porting to Hugo.

## Regenerating these HTMLs

If the Excel is updated, regenerate everything by running:

```bash
python3 ../translate_hetzner.py
```

(Path is relative to this folder; the script lives one level up.)
