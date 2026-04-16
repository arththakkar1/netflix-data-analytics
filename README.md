# Netflix Data Analytics

A comprehensive data cleaning and preprocessing pipeline for Netflix's dataset, transforming raw data into analysis-ready format.

## 📋 Project Overview

This project processes Netflix content data to prepare it for analysis and visualization. It handles data quality issues, performs feature engineering, and standardizes the dataset for downstream analytics.

### Key Features

- **Data Loading**: Reads Netflix CSV dataset
- **Missing Value Handling**: Intelligent imputation strategies for different column types
- **Feature Engineering**: Extracts meaningful features from raw data
- **Data Cleaning**: Standardizes formats, removes whitespace, validates data types
- **Data Expansion**: Explodes multi-value columns for granular analysis
- **Export**: Outputs cleaned dataset in CSV format

## 📊 Dataset Structure

### Original Columns

- `show_id`: Unique identifier for each show/movie
- `type`: Movie or TV Show
- `title`: Name of the content
- `director`: Director(s) of the content
- `cast`: Actor(s) in the content
- `country`: Country/Countries of origin
- `date_added`: Date content was added to Netflix
- `release_year`: Original release year
- `rating`: Content rating (TV-MA, TV-14, PG-13, etc.)
- `duration`: Length of content (in minutes for movies, seasons for TV shows)
- `listed_in`: Genre/Categories
- `description`: Plot description

### Engineered Features

- `year_added`: Extracted year from `date_added`
- `duration_num`: Numeric duration extracted from `duration` column
- `duration_type`: Type of duration (Minutes or Seasons)

### Handling of Multi-Value Columns

- **country**: Split by comma and exploded into separate rows for country-level analysis
- Multiple rows created for content available in multiple countries

## 🔧 Data Processing Pipeline

### Phase 1: Initial Cleaning

1. Fill missing values in categorical columns with "Unknown"
2. Handle missing `rating` with mode (most frequent value)
3. Split and explode `country` column for multi-country content

### Phase 2: Feature Engineering

- Extract numeric duration and duration type
- Parse and extract year from date_added
- Strip whitespace from text fields

### Phase 3: Final Validation

- Complete remaining missing value handling
- Fill `duration_type` with "Unknown"
- Set default date for missing `date_added` (1900-01-01)

## 📁 Files Description

| File                   | Description                                                  |
| ---------------------- | ------------------------------------------------------------ |
| `app.ipynb`            | Main Jupyter notebook with complete data processing pipeline |
| `netflix.csv`          | Original unprocessed Netflix dataset                         |
| `netflix_filtered.csv` | Cleaned and processed dataset ready for analysis             |
| `README.md`            | This file - project documentation                            |

## 🚀 Usage

### Prerequisites

- Python 3.7+
- pandas library

### Installation

```bash
pip install pandas jupyter
```

### Running the Notebook

1. Open the project directory in Jupyter Notebook or VS Code
2. Open `app.ipynb`
3. Run cells sequentially or use "Run All" to execute the entire pipeline
4. The script will generate `netflix_filtered.csv` with the cleaned data

```bash
jupyter notebook app.ipynb
```

## 📈 Data Quality Improvements

### Missing Values Handling

| Column     | Missing Count | Handling Strategy        |
| ---------- | ------------- | ------------------------ |
| director   | High          | "Unknown"                |
| cast       | High          | "Unknown"                |
| country    | Low           | "Unknown" + Explode      |
| rating     | Low           | Mode/Most frequent value |
| listed_in  | Medium        | "Unknown" + Strip spaces |
| date_added | Medium        | 1900-01-01               |
| duration   | Low           | "0 min"                  |

### Data Type Conversions

- `date_added`: String → DateTime
- `year_added`: Extracted → Integer
- `duration_num`: Extracted from string → Float
- `duration_type`: Extracted → String

## 📊 Output Dataset Features

After processing, the cleaned dataset includes:

- **Total Rows**: Increased due to country expansion (one row per country)
- **Complete Data**: Zero missing values
- **Standardized Format**: Consistent data types and formats
- **Enhanced Features**: New engineered columns for analysis
- **Ready for Analysis**: Can be used for:
  - Content type distribution analysis
  - Release trends over time
  - Rating analysis
  - Country-based content insights
  - Duration analysis by content type
  - Genre analysis

## 🔍 Example Analysis Queries

With the cleaned data, you can answer:

- How many movies vs TV shows are available?
- What are the most common ratings?
- Which countries produce the most content?
- How has Netflix's content library grown over time?
- What's the average duration of content by type?
- What genres are most prevalent?

## 📝 Code Structure

The notebook is organized into 14 clear steps:

1. **Import Libraries**: Load pandas
2. **Load Data**: Read Netflix CSV
3. **Check Missing Values**: Initial assessment
4. **Check Data Types**: Validate column types
5. **Phase 1 Imputation**: Fill missing categorical values
6. **Expand Countries**: Split multi-country entries
7. **Feature Engineering**: Extract new features
8. **Validate Phase 1**: Check progress
9. **Phase 2 Imputation**: Handle remaining nulls
10. **Validate Phase 2**: Final null check
11. **Handle Duration Type**: Fill remaining nulls
12. **Handle Date Added**: Set default dates
13. **Final Verification**: Confirm complete cleaning
14. **Export**: Save cleaned CSV

## 🔄 Processing Flow Diagram

```
Raw CSV → Load Data → Explore Data → Check Nulls → Fill Nulls (Phase 1)
    ↓
Split Countries → Feature Engineering → Validate → Fill Nulls (Phase 2)
    ↓
Handle Types → Set Defaults → Final Check → Export CSV
```

## 💡 Key Insights from Processing

- **Data Quality**: The dataset had moderate missing values requiring strategic imputation
- **Multi-valued Fields**: Country information required expansion for proper analysis
- **Feature Creation**: Extracted year and numeric values enable time-series and numeric analysis
- **Data Standardization**: Consistent handling ensures reliable downstream analysis

## 🛠️ Customization

To modify the processing pipeline:

1. **Change Missing Value Strategy**: Edit Phase 1/2 filling logic
2. **Adjust Split Character**: Change `", "` to different delimiter in country split
3. **Filter Data**: Add filters before export based on specific criteria
4. **Add Features**: Create additional engineered columns as needed

## ⚠️ Data Assumptions

- Data quality improves with updates to the original dataset
- "Unknown" values are treated as valid categories during analysis
- Date before 1900 treated as missing
- All multi-country assignments are valid
- Duration types are either Minutes or Seasons

## 📌 Notes

- The dataset is updated periodically as Netflix adds/removes content
- Analysis results may vary with dataset date
- Some historical data may be incomplete
- Recommendations: Filter by relevant date ranges for time-series analysis

## 📞 Support & Contributions

For questions or improvements to the processing pipeline:

1. Check the notebook comments for implementation details
2. Verify data assumptions match your analysis needs
3. Test filtering logic with sample data first

---

**Last Updated**: April 2026
**Dataset Source**: Netflix
**Processing Framework**: Python + Pandas
