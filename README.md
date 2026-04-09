# MSEF 2026 High School Abstracts Survey

A lightweight, reproducible repository for extracting and summarizing **school-wise abstract counts by domain** from the uploaded PDF **`2026HS-Abstract-final.pdf`**.

## Overview

This project parses the 2026 Massachusetts Science & Engineering Fair (MSEF) high school abstract book and produces a clean, analysis-ready dataset in the format:

```text
School | Domain | Count
```

The repository is designed for:

- quick review of which schools appear in the abstract book,
- counting how many abstracts each school has in each domain,
- generating reusable CSV and Markdown summaries,
- sharing the workflow on GitHub with minimal setup.

## Repository Structure

```text
msef-school-domain-summary/
├── README.md
├── requirements.txt
├── .gitignore
├── data/
│   ├── abstract_index.csv
│   ├── school_domain_counts.csv
│   ├── school_domain_counts.md
│   └── school_totals.csv
├── scripts/
│   └── parse_msef_abstracts.py
└── wiki/
    ├── Home.md
    ├── Data-Dictionary.md
    ├── Methodology.md
    └── Usage.md
```

## Included Outputs

### `data/abstract_index.csv`
One row per parsed abstract page.

**Columns**
- `page` — page number in the PDF
- `project_code` — abstract/project code (example: `AB-01-BE`)
- `domain` — domain/category extracted from the page
- `school` — school name extracted from the page
- `title` — project title

### `data/school_domain_counts.csv`
The main output table.

**Columns**
- `school`
- `domain`
- `count`

This file is **alphabetically sorted by school**, then by domain.

### `data/school_totals.csv`
Total number of parsed abstracts for each school across all domains.

### `data/school_domain_counts.md`
Markdown version of the school-domain count table for easy viewing in GitHub.

## How It Works

The parser uses **PyMuPDF** to read the PDF page-by-page and extract the first few lines of each abstract page.

For each valid abstract page, the script assumes the following structure:

1. **Project code**
2. **Domain**
3. **School**
4. **Title**

If the first line matches a project-code pattern such as:

- `AB-01-BE`
- `GBR-117-MA`
- `JBR-07-CS`

then the page is treated as a valid abstract page and included in the dataset.

The parsed records are then aggregated into:

- a detailed abstract index,
- a school-by-domain count table,
- a school total summary.

## Quick Start

### 1. Clone the repository

```bash
git clone <your-repo-url>
cd msef-school-domain-summary
```

### 2. Create and activate a virtual environment

**macOS / Linux**

```bash
python -m venv .venv
source .venv/bin/activate
```

**Windows**

```powershell
python -m venv .venv
.venv\Scripts\activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Place the PDF in the repository root

Expected file name:

```text
2026HS-Abstract-final.pdf
```

### 5. Run the parser

```bash
python scripts/parse_msef_abstracts.py
```

## Example Output

Example rows from `school_domain_counts.csv`:

```text
Acton-Boxborough Regional High | Biochemistry | 1
Acton-Boxborough Regional High | Biology: Cellular, Molecular, or Microbiology | 1
Acton-Boxborough Regional High | Computer Science and Technology | 3
Al Noor Academy | Behavioral and Social Sciences | 1
Boston Latin School | Biochemistry | 1
```

## Dependencies

Minimal dependencies are required:

```text
pandas
PyMuPDF
```

Install them with:

```bash
pip install -r requirements.txt
```

## Reproducibility Notes

- This parser is tailored to the current layout of the uploaded PDF.
- If future abstract books change the page header order or formatting, the parsing logic may need a small update.
- The dataset reflects what is parsable directly from the PDF; it is not intended as a separate authoritative source beyond the document itself.

## Suggested GitHub Topics

If you publish this repo, these topics may help discovery:

- `pdf-parsing`
- `pymupdf`
- `pandas`
- `data-cleaning`
- `science-fair`
- `education-data`
- `massachusetts`
- `csv`

## Future Enhancements

Possible next improvements:

- add a **GitHub Actions** workflow to regenerate outputs automatically,
- export an **Excel workbook** with separate tabs,
- build a **pivot table** summary,
- publish a **GitHub Pages** dashboard,
- include validation checks for duplicate project codes.

## License

You can add a license depending on how you want to share the project, for example:

- MIT License
- Apache-2.0
- Creative Commons (for documentation/data)

## Contact / Usage

This repository is intended as a clean, shareable summary project for the uploaded MSEF abstract PDF. If you adapt it for a different abstract book, update:

- the input PDF name,
- the header matching regex,
- and any page-structure assumptions in `scripts/parse_msef_abstracts.py`.
