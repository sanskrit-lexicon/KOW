_Created: 15-05-2026 · Last updated: 05-09-2026_

# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**KOW** is the corrections repository for the Cologne digitization of Kossowich's *Sanskrito-russkiy slovar* (Sanskrit-Russian Dictionary, 1854). It is part of the [Cologne Digital Sanskrit Dictionaries](https://www.sanskrit-lexicon.uni-koeln.de/) project.

- **Org**: [sanskrit-lexicon](https://github.com/sanskrit-lexicon)
- **Input file**: `csl-orig/v02/kow/kow.txt` (in the `csl-orig` sibling repo)
- **Scan repository**: `KOWScan`
- **Language pair**: Sanskrit → Russian
- **Entries**: ~13,488 L-entries across 360 pages (2 columns)

Issues and corrections for this dictionary are tracked in the [GitHub issue tracker](https://github.com/sanskrit-lexicon/KOW/issues).

## Architecture

| Path | Role |
|---|---|
| `csl-orig/v02/kow/kow.txt` | Primary source file (in sibling repo) |
| `csl-pywork/v02/` | Python build scripts, `generate_dict.sh`, `xmlchk_xampp.sh` |
| `KOWScan/` | PNG page scans of the printed dictionary |

## Common Commands

### Apply line-level corrections (standard pattern)
```bash
python updateByLine.py <input_file> <changefile> <output_file>
```

Change file format — paired lines, `;` prefix for comments:
```
1234 old original line text here
1234 new replacement line text here
```
Supports `new` (replace), `ins` (insert after), `del` (delete). All files UTF-8.

### Rebuild and validate XML (from `csl-pywork/v02/`)
```bash
sh generate_dict.sh kow ../../KOWScan/2020
sh xmlchk_xampp.sh kow
```

## Dependencies

- **Python 3** with `sys.stdout.reconfigure(encoding='utf-8')` in all scripts
- **kow.txt** — in `$BASE/cologne/csl-orig/v02/kow/kow.txt`
- **csl-pywork** — sibling repo containing build toolchain

## Data Format

Every entry in `kow.txt` follows the Cologne markup format:

| Tag | Role | Example |
|---|---|---|
| `<L>NNNN` | Entry begin, with print line number | `<L>12345` |
| `<LEND>` | Entry end | |
| `<k1>headword` | Primary headword in SLP1 | `<k1>rAma` |
| `<k2>variant` | Secondary spelling | `<k2>rAma` |
| `<e>N` | Etymology/sub-entry marker | `<e>1` |
| `<lex>code` | Lexical category | `<lex>m.` |
| `<ls>source` | Literary source citation | `<ls>Rv. 1,22,16` |
| `<ab>tag` | Italicised abbreviation | `<ab>m.</ab>` |
| `{#text#}` | Sanskrit text in SLP1 | `{#rAmaH#}` |
| `{%text%}` | Italicised display text | `{%abc%}` |

### Annotated example entry

```
<L>42<pc>5,1<k1>aMSa<k2>aMSa
{#aMSa#}¦ <lex>m.</lex> плечо; доля; часть. <ls>Mn.</ls>
<LEND>
```

- `<L>42` — entry number 42
- `<pc>5,1` — page 5, column 1 of the print
- `<k1>aMSa` — headword in SLP1 (`aMSa` = अंश)
- `{#aMSa#}` — Sanskrit text for display
- `<lex>m.</lex>` — masculine noun
- Russian definitions follow the bar (`¦`)
- `<ls>Mn.</ls>` — citation to Manusmriti

## GitHub Issue Conventions

### Milestones

| # | Milestone | Scope |
|---|---|---|
| 1 | Dictionary to Book | Link targets and link splitting |
| 2 | Digitization Quality | Scan quality, encoding, bug fixes, text corrections |
| 3 | Structured Data | Markup normalisation, structured data, editorial questions |
| 4 | Major Enhancements | Large new content, display upgrades, new versions |

### Type labels (color `#0075ca`)

| Label | When to use |
|---|---|
| `link-target` | Building click-throughs from `<ls>` abbreviations to scanned PDF pages |
| `link-splitting` | Splitting combined `SOURCE N,N` refs into individual per-page links |
| `markup` | Normalising XML tag content (`<ls>`, `<lex>`, `<ab>`, etc.) |
| `text-correction` | Corrections to Russian definitions or Sanskrit headwords |
| `content-enhancement` | New material, display upgrades, structural additions beyond correction |
| `encoding` | SLP1/AS/IAST transcoding, character rendering, hyphen/dash normalisation |
| `scan-quality` | Replacing blurry, skewed, or missing scan pages |
| `bug` | Broken links, XML errors, broken download files |
| `question` | Scholarly questions requiring research before any code change |

### Severity labels

| Label | Color | When to use |
|---|---|---|
| `minor` | `#e4e669` | Targeted, self-contained fix |
| `medium` | `#fbca04` | Standard unit of work — one index, a batch of corrections |
| `hard` | `#d93f0b` | Large effort spanning many sources, files, or dictionaries |

_Dr. Mārcis Gasūns_
