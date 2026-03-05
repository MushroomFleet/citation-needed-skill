# Citation-Needed Skill

A Claude skill that accepts articles, reports, and documents, verifies every factual claim via web search, and produces a standalone `_citation.md` report alongside your original file — without ever modifying it.

There is an optional ["Collect Citations" skill](https://github.com/MushroomFleet/collect-citations-skill) which is designed to work with the output from this skill.

---

## What It Does

Drop in any document and Citation-Needed will scan it for verifiable claims — statistics, figures, named studies, attributed quotes, dates, rankings, and regulatory references — then research each one and produce a clean citation report.

The `_citation.md` report contains:

- **Confirmed citations** — verified facts with authoritative source URLs
- **Near misses** — facts that exist but carry wrong figures, dates, scope, or units, with corrections and sources
- **Unverified claims** — flagged with the search queries attempted, ready for author review
- **A research task log** — a dynamic checklist showing every claim searched, making the process fully auditable
- **A URL reference index** — every source cited by a sequential ID (`url_01`, `url_02`, ...)

---

## How It Works

1. **Index** — the input file is read and every line is numbered before any processing begins
2. **Extract** — every verifiable claim is identified with its exact line number(s)
3. **Research** — each claim is searched using 2–3 targeted queries against authoritative sources
4. **Classify** — each result is graded: Confirmed ✅, Near Miss ⚠️, Superseded 🔁, or Unverified ❓
5. **Report** — a `_citation.md` file is written with all findings; the original is untouched

---

## Output: The `_citation.md` Report

### Confirmed Citations
Each confirmed claim links to its authoritative source with publication name, URL, and source date.

### Near Misses
The most valuable output. Near misses appear in a scannable inline format:

```
Line 54: "55 million in 2024" - figure should read "56.5 million in 2025" [url_04]
```

Every near miss entry includes the discrepancy type (figure delta, temporal drift, scope mismatch, unit error, or attribution shift) so you know exactly what needs fixing.

### Unverified Claims
Claims where no authoritative source was located are listed with all queries attempted and a recommendation (remove, qualify, or find a primary source).

### URL Reference Index

| ID | Source | URL | Accessed |
|---|---|---|---|
| url_01 | WHO | https://... | 2025-06-01 |
| url_02 | ONS | https://... | 2025-06-01 |

---

## Installation

### Claude.ai Web or Claude Code (Upload)

1. Download `citation-needed.skill` from this repository
2. In **Claude.ai**: open Settings → Skills → Upload Skill
3. In **Claude Code**: use the Skills panel or drag the file into the interface
4. The skill is immediately active — no restart required

### CLI Installation (Claude Code)

The `.skill` file is a standard ZIP archive. Unzip it directly into the Claude Code commands directory:

```bash
unzip citation-needed.skill -d ~/.claude/commands/citation-needed
```

Then restart Claude Code or run `/reload-skills` to activate.

### Manual ZIP Extraction

If your system requires an explicit `.zip` extension:

```bash
cp citation-needed.skill citation-needed.zip
unzip citation-needed.zip -d ~/.claude/commands/citation-needed
```

---

## Usage

The skill triggers automatically when you upload a document alongside any of these kinds of requests:

- *"citation needed"*
- *"check citations"*
- *"verify sources"*
- *"fact check this"*
- *"find sources for this article"*
- *"add citations to this"*
- *"check the facts in this document"*
- *"verify this document"*
- *"check my figures"*
- *"source check"*

### Example Session

```
User: Can you fact-check this report for me?
[attaches quarterly-report.md]

Claude reads the skill → indexes all lines → extracts 14 claims →
searches each claim → classifies outcomes → writes report

Output: quarterly-report_citation.md
Claims detected: 14 | Confirmed: 9 | Near misses: 3 | Unverified: 2
```

---

## File Naming

| Input File | Output File |
|---|---|
| `report.md` | `report_citation.md` |
| `whitepaper-v2.txt` | `whitepaper-v2_citation.md` |
| `Q3 Analysis.docx` | `Q3 Analysis_citation.md` |

The citation report is always placed in the same directory as the input file.

---

## Notes

- **Non-destructive** — the input file is never modified under any circumstances
- Paywalled sources are still cited; access status is noted in the report
- When two authoritative sources conflict, both are reported with a conflict note
- Duplicate claims (same fact on multiple lines) produce one entry with all line references
- The research task log is dynamic — generated per document, not a static template

---

## 📚 Citation

### Academic Citation

If you use this codebase in your research or project, please cite:

```bibtex
@software{citation_needed_skill,
  title = {Citation Needed Skill: A Claude skill for verifying and citing factual claims in documents},
  author = {[Drift Johnson]},
  year = {2025},
  url = {https://github.com/MushroomFleet/citation-needed-skill},
  version = {1.0.0}
}
```

### Donate:

[![Ko-Fi](https://cdn.ko-fi.com/cdn/kofi3.png?v=3)](https://ko-fi.com/driftjohnson)
