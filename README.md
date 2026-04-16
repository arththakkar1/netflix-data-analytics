# Netflix Data Analytics

A complete end-to-end data analytics project covering raw data cleaning, preprocessing, and interactive dashboard visualization for Netflix's content dataset.

---

## Project Overview

This project is structured in two stages. The first stage is a Python-based data cleaning and preprocessing pipeline that transforms raw Netflix CSV data into an analysis-ready format. The second stage is a Power BI dashboard that visualizes the cleaned data through an interactive interface designed to reflect Netflix's visual identity.

---

## Dashboard

The Power BI dashboard was built on top of the cleaned dataset and follows a strict three-color design system:

- **Charcoal black** as the base background, mirroring Netflix's dark interface
- **Netflix red (#E50914)** applied uniformly across all chart elements — bars, lines, and donut segments — so color carries a single, consistent meaning
- **White** reserved exclusively for text, KPI values, and labels for maximum readability

### Dashboard Components

| Visual                 | Description                                                                             |
| ---------------------- | --------------------------------------------------------------------------------------- |
| KPI Cards              | Total Movies (7,814), Total TV Shows (3,031), Latest Year (2021), Recent Titles (6,741) |
| Movies vs TV Shows     | Donut chart showing 72.05% Movies and 27.95% TV Shows                                   |
| Top 10 Countries       | Horizontal bar chart of countries with the highest content volume                       |
| Titles by Release Year | Line chart showing Netflix content growth over time                                     |
| Rating Distribution    | Bar chart ordered by content rating frequency                                           |
| Filters                | Interactive slicers for Type, Rating, and Release Year                                  |

---

## Data Pipeline

### Dataset Structure

**Original Columns**

| Column         | Description                         |
| -------------- | ----------------------------------- |
| `show_id`      | Unique identifier for each title    |
| `type`         | Movie or TV Show                    |
| `title`        | Name of the content                 |
| `director`     | Director(s)                         |
| `cast`         | Actor(s)                            |
| `country`      | Country/countries of origin         |
| `date_added`   | Date added to Netflix               |
| `release_year` | Original release year               |
| `rating`       | Content rating (TV-MA, PG-13, etc.) |
| `duration`     | Length in minutes or seasons        |
| `listed_in`    | Genre/categories                    |
| `description`  | Plot description                    |

**Engineered Features**

| Column          | Description                             |
| --------------- | --------------------------------------- |
| `year_added`    | Extracted year from `date_added`        |
| `duration_num`  | Numeric value extracted from `duration` |
| `duration_type` | Type of duration — Minutes or Seasons   |

---

## Data Processing Pipeline

### Phase 1 — Initial Cleaning

1. Fill missing values in categorical columns with "Unknown"
2. Handle missing `rating` with mode (most frequent value)
3. Split and explode `country` column for multi-country content

### Phase 2 — Feature Engineering

- Extract numeric duration and duration type
- Parse and extract year from `date_added`
- Strip whitespace from all text fields

### Phase 3 — Final Validation

- Complete remaining missing value handling
- Fill `duration_type` with "Unknown"
- Set default date for missing `date_added` (1900-01-01)

---

## Data Quality Improvements

### Missing Values Handling

| Column       | Missing Count | Handling Strategy          |
| ------------ | ------------- | -------------------------- |
| `director`   | High          | "Unknown"                  |
| `cast`       | High          | "Unknown"                  |
| `country`    | Low           | "Unknown" + Explode        |
| `rating`     | Low           | Mode / most frequent value |
| `listed_in`  | Medium        | "Unknown" + strip spaces   |
| `date_added` | Medium        | 1900-01-01                 |
| `duration`   | Low           | "0 min"                    |

### Data Type Conversions

| Column          | From      | To       |
| --------------- | --------- | -------- |
| `date_added`    | String    | DateTime |
| `year_added`    | Extracted | Integer  |
| `duration_num`  | String    | Float    |
| `duration_type` | Extracted | String   |

---

## Processing Flow

```
Raw CSV → Load Data → Explore → Check Nulls → Fill Nulls (Phase 1)
    ↓
Split Countries → Feature Engineering → Validate → Fill Nulls (Phase 2)
    ↓
Handle Types → Set Defaults → Final Check → Export CSV → Power BI Dashboard
```

---

## Files

| File                   | Description                                                  |
| ---------------------- | ------------------------------------------------------------ |
| `app.ipynb`            | Main Jupyter notebook with complete data processing pipeline |
| `netflix.csv`          | Original unprocessed Netflix dataset                         |
| `netflix_filtered.csv` | Cleaned and processed dataset ready for analysis             |
| `Netflix.pbix`         | Power BI dashboard file                                      |
| `README.md`            | Project documentation                                        |

---

## Usage

### Prerequisites

- Python 3.7+
- pandas
- Power BI Desktop (for the dashboard)

### Installation

```bash
pip install pandas jupyter
```

### Running the Notebook

1. Open the project directory in Jupyter Notebook or VS Code
2. Open `app.ipynb`
3. Run cells sequentially or use "Run All"
4. The script will generate `netflix_filtered.csv`

```bash
jupyter notebook app.ipynb
```

### Opening the Dashboard

1. Install [Power BI Desktop](https://powerbi.microsoft.com/desktop/)
2. Open `Netflix.pbix`
3. If prompted, reconnect the data source to the local `netflix_filtered.csv` file

---

## Notebook Structure

The notebook is organized into 14 steps:

1. Import Libraries
2. Load Data
3. Check Missing Values
4. Check Data Types
5. Phase 1 Imputation
6. Expand Countries
7. Feature Engineering
8. Validate Phase 1
9. Phase 2 Imputation
10. Validate Phase 2
11. Handle Duration Type
12. Handle Date Added
13. Final Verification
14. Export

---

## Data Assumptions

- "Unknown" values are treated as valid categories during analysis
- Dates before 1900 are treated as missing
- All multi-country assignments are considered valid
- Duration types are either Minutes or Seasons
- The dataset reflects a specific snapshot of Netflix's catalog and may not represent its current library

---

## Notes

- The dataset is periodically updated as Netflix adds and removes content
- Analysis results may vary depending on the dataset version
- For time-series analysis, filtering by relevant date ranges is recommended
- Some historical records may contain incomplete metadata
