# Sanctions Test Files Generator

A standalone browser-based tool to generate sanctions screening test files from the **UN Consolidated Sanctions List** and **local 1373 lists**. No installation, no server, no dependencies — just open the HTML file in any browser.

---

## What it does

Generates structured CSV test files that can be fed directly into automated screening test runners (e.g. Playwright-based). Each file tests a specific matching scenario:

| Category | Description |
|---|---|
| Cat 1 – Exact match | Verbatim names and aliases |
| Cat 2 – Spelling variants | Common misspellings — vowel changes, doubled or dropped letters, similar-sounding substitutions |
| Cat 3 – Name order transposed | Tokens rearranged with a slight spelling variation |
| Cat 4 – Partial names | Subsets of names with 3+ tokens |
| Cat 5 – Diacritics / special chars | Normalised versions of names containing accents, hyphens, or apostrophes |
| ID list | Extracted and normalised document ID numbers |

All generated variants are **pre-validated** against the fuzzy matching pipeline before inclusion — only variants that would genuinely match in the screening system are included.

---

## How to use

### UN Consolidated List tab
1. Download the latest XML from [scsanctions.un.org](https://scsanctions.un.org/resources/xml/en/consolidated.xml)
2. Open `un_sanctions_test_generator.html` in any browser
3. Click **Choose file** and select the XML — the list date and name count appear instantly
4. Click **Generate** on any category, optionally adjusting variants per name (1–5)
5. Click **Download CSV**

### Local 1373 List tab
1. Click **Choose file** under Individuals and/or Entities to load your Excel files
2. Columns used:
   - Individuals: Reference Number, Name, DL/Passport No., NIC No.
   - Entities: Reference Number, Name, Registration No.
3. Names with a.k.a. variants (including misspelled variants like `a.ka.`, `ak.a`) are automatically split
4. Generate and download test files for any category

### Running the tests
Feed generated CSV into any automated testing script such as Playwright:

---

## Technical notes

- **No installation required** — single HTML file, runs entirely in the browser
- **No data leaves your machine** — all processing is local JavaScript
- **Excel support** — SheetJS is loaded from CDN on first use (internet connection required for local list tab)
- **Fuzzy scoring engine** — embeds a full JavaScript port of the Python fuzzy matching pipeline, including the discriminating token penalty and four matching rules, so generated variants are validated before inclusion
- **Name normalisation** — apostrophes are removed, diacritics are stripped, hyphens become spaces — consistent with a typical screening system's normaliser

---

## Files

| File | Description |
|---|---|
| `index.html` | The tool — open this in a browser |
| `README.md` | This file |

---

## Developer

[Kosala Harshadewa](https://www.linkedin.com/in/kosala-harshadewa) — Financial Intelligence Unit Strengthening Project, Maldives (UNODC)

---

## License

MIT License — free to use, modify, and distribute.
