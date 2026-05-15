# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**KOW** is the corrections repository for the Cologne digitization of Kossowich's *Sanskrit-Russian Dictionary*. The canonical source lives in `csl-orig/v02/kow/kow.txt`.

Issues and corrections for this dictionary are tracked in the [GitHub issue tracker](https://github.com/sanskrit-lexicon/KOW/issues).

## Common Commands

### Apply line-level corrections (standard pattern)
```bash
python updateByLine.py <input_file> <changein_file> <output_file>
```

### Rebuild and validate XML (from `csl-pywork/v02/`)
```bash
sh generate_dict.sh kow ../../KOWScan/2020
sh xmlchk_xampp.sh kow
```

## Dependencies

- **Python 3**
- **kow.txt** — in `$BASE/cologne/csl-orig/v02/kow/kow.txt`
