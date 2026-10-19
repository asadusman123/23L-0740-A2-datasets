# 23L-0740 — Assignment 2 cleaned datasets

Cleaned datasets produced for **Assignment 2 (Exploratory Data Analysis)** by Asad Usman (23L-0740, BSCS-7H, FAST-NUCES Lahore).
They are the fixed inputs for **Assignment 3 (Feature Selection and Dimensionality Reduction)**.

| File | Rows × columns | Version | Date |
|---|---|---|---|
| `23L_0740_A2_netflix_cleaned.csv` | 8,806 × 25 | v1.0 | 2026-10-19 |
| `23L_0740_A2_supermarket_cleaned.csv` | 1,000 × 25 | v1.0 | 2026-10-19 |

Load a fixed version in Assignment 3 with the tag in the URL, for example:

```python
import pandas as pd
base = 'https://raw.githubusercontent.com/asadusman123/23L-0740-A2-datasets/v1.0/'
netflix = pd.read_csv(base + '23L_0740_A2_netflix_cleaned.csv', parse_dates=['date_added'])
supermarket = pd.read_csv(base + '23L_0740_A2_supermarket_cleaned.csv', parse_dates=['Date', 'Datetime'])
```

## Sources

- **Netflix:** *Netflix Movies and TV Shows*, Shivam Bansal, Kaggle — https://www.kaggle.com/datasets/shivamb/netflix-shows (`netflix_titles.csv`, 8,807 × 12). Credit to the original author; reuse is subject to the licence stated on the Kaggle page.
- **Supermarket Sales:** `supermarket_Sales.csv` (1,000 × 17), provided by the course instructor, used exactly as supplied.

## What changed

### Netflix (v1.0)
- Stripped whitespace from all text fields (88 `date_added` values had a leading space; 1 title had a trailing space).
- Removed 1 exact duplicate (*Consequences*, s6530), which was identical to s3372 once the whitespace was removed → 8,806 rows. Kept 3 case-variant re-listings that have different dates.
- Moved 3 durations (`74/84/66 min`) out of `rating` back into `duration`.
- Merged rating `UR` into `NR`. Missing ratings (7 in total, including the 3 above) are labelled `Unknown`.
- Filled missing `director` (2,634), `cast` (825) and `country` (831) with `Unknown`. Removed empty items from comma-separated lists.
- Converted `date_added` to ISO dates (`YYYY-MM-DD`). The 10 missing values are left empty.
- **Added columns:** `movie_minutes`, `seasons`, `year_added`, `month_added`, `lag_years`, `added_before_release`, `n_countries`, `n_genres`, `n_cast`, `n_directors`, `primary_country`, `primary_genre`, `rating_group`.
- **How to read the new columns:** `n_*` = 0 means the value was not recorded. `movie_minutes` is empty for TV shows and `seasons` is empty for movies, by design.
- No outliers were removed.

### Supermarket Sales (v1.0)
- No missing values, duplicates or invalid values were found, so no rows were removed and no values were altered.
- `Date` is converted to ISO format (`YYYY-MM-DD`); `Time` is kept as `HH:MM`.
- **Added columns:** `Datetime`, `Hour`, `Month`, `Month name`, `Day of week`, `Day of week num`, `Is weekend`, `Time of day`.
- **Redundant original columns, kept on purpose:** `Cost of goods sold`, `Tax 5%`, `Total` and `Gross income` are exact functions of `Unit price` × `Quantity`. `Gross margin percentage` is constant. `City` maps one-to-one to `Branch`.

## Versioning
`v1.0` is the version used in Assignment 2. Any later change to the cleaning will be published as a new tag (`v1.1`, …) with its changes listed here. Earlier tags will not be overwritten.
