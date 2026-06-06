---
{
  "id": "file_jozdtsre",
  "filetype": "document",
  "filename": "README",
  "created_at": "2026-06-06T00:59:55.457Z",
  "updated_at": "2026-06-06T01:02:54.742Z",
  "meta": {
    "location": "/",
    "tags": [],
    "categories": [],
    "description": "",
    "source": "markdown"
  }
}
---
# Google Sheets Placement Preference Sorter

This Google Apps Script sorts first-year medical school programme rows from **most preferred** to **least preferred** based on the placement preferences you enter.

It is designed for a Google Sheet where each programme row contains:

- A unique programme code, such as `FY1-26-001`
- Four placement columns, one for each quarter
- A rank column where the final preference order is written

## Installation

1. Open the Google Sheet.
2. If the file still says `.XLSX` beside the name, click **File &gt; Save as Google Sheets** first.
3. Go to **Extensions &gt; Apps Script**.
4. Paste the contents of `scripts/placement-preference-sorter.gs` into the Apps Script editor.
5. Save the project.
6. Reload the Google Sheet.
7. Give permissions to the script 
8. Use the new **Placement Sorter** menu.

## How To Use

1. Click **Placement Sorter &gt; Create / Refresh Setup Sheets**.
2. Open the **Sorter Settings** tab and check the settings.
3. Open the **Preferences** tab.
4. Reorder column `B` so your favourite placement is at the top and your least favourite is at the bottom.
5. Click **Placement Sorter &gt; Sort Programmes by Preferences**.

## Non-Coder Settings

The **Sorter Settings** tab lets you customise the sorter without editing code.

| Setting | What It Means | Default |
|---|---|---:|
| Target sheet name | The tab containing the programme table. Leave blank to use the first normal sheet. | blank |
| First data row | First row containing a programme. | `3` |
| Rank column | Column where rank numbers should be written. | `E` |
| Programme code column | Column containing codes like `FY1-26-001`. | `F` |
| First placement column | First quarter placement column. | `G` |
| Number of placement columns | Number of placement columns to score. | `4` |
| Rank header cell | Cell containing the rank column heading. | `E1` |
| Preference weighting strength | How strongly top preferences are prioritised. | `2` |
| Preserve colours and text styling | Whether colours/fonts move with each programme row. | `Yes` |

## Weighting Guide

**Preference weighting strength** controls how much the top preferences dominate the ranking.

| Value | Weighting | What It Does |
|---:|---|---|
| `1` | Gentle | Balanced rows can compete with rows containing one top choice. |
| `2` | Balanced | Good default for most users. |
| `3` | Strong | Top choices have a much bigger effect. |
| `4` | Very strong | Best if you want top choices to dominate heavily. |

## How Ranking Works

Each programme row gets a weighted score from the four placement columns.

Top preferences receive more points than lower preferences, so programmes containing your favourite placements are more likely to appear near the top.

For example, if your preferences are:

```text
Medicine
Surgery
Cardiology
Urology
```

Then:

| Placement | Priority |
|---|---:|
| Medicine | Highest |
| Surgery | Second highest |
| Cardiology | Third highest |
| Urology | Fourth highest |

The programme row with the **highest total weighted score** is ranked highest.

Ties are broken by:

1. Best individual placement in the row
2. Second-best individual placement in the row
3. Programme code

## Important Note

Run this on a copy of your spreadsheet first.

It is highly recommended that you manually review the file before submitting in case of any mismatch in settings vs what is on your version fo the docs :D \
\
Best of luck!