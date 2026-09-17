# Amazon Prime Movies and TV Shows – Exploratory Data Analysis (EDA)

![Python](https://img.shields.io/badge/Python-3.11-blue.svg)
![Pandas](https://img.shields.io/badge/Pandas-2.0%2B-150458.svg)
![Seaborn](https://img.shields.io/badge/Seaborn-0.13%2B-blueviolet.svg)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)

An end-to-end Exploratory Data Analysis project analyzing Amazon Prime Video's content catalog using genuine streaming metadata.

---

## 1. Project Overview
Amazon Prime Video is one of the world's largest streaming and video-on-demand platforms, hosting thousands of feature films, episodic television series, documentaries, and regional programming. This project conducts a systematic exploratory analysis into the composition, historical trends, audience ratings, runtimes, genre distribution, production geography, and leading talent across the platform's catalog.

---

## 2. Project Objective
> *The objective of this project is to analyze Amazon Prime movies and TV shows and identify patterns in content type, release years, genres, ratings, runtimes, production countries, and cast information using Exploratory Data Analysis techniques.*

---

## 3. Dataset Descriptions
The project utilizes two real-world datasets:

1. **`titles.csv`** (9,871 records, 15 attributes):
   - `id`: Unique identifier for each title (e.g., `tm19248`, `ts20945`).
   - `title`: Name of the movie or TV show.
   - `type`: Content category (`MOVIE` or `SHOW`).
   - `description`: Plot synopsis or brief storyline.
   - `release_year`: Year of initial release (ranging from vintage cinema to 2022).
   - `age_certification`: Maturity rating (e.g., `TV-MA`, `PG-13`, `R`).
   - `runtime`: Duration in minutes.
   - `genres`: Stringified Python list of applicable genres.
   - `production_countries`: Stringified Python list of ISO country codes.
   - `seasons`: Total seasons (applicable to TV shows; null for movies).
   - `imdb_id`: Alphanumeric IMDb reference code.
   - `imdb_score`: Weighted user rating on IMDb (scale 1.0 to 10.0).
   - `imdb_votes`: Number of user rating votes cast on IMDb.
   - `tmdb_popularity`: Rolling popularity index calculated by The Movie Database.
   - `tmdb_score`: User score on TMDB.

2. **`credits.csv`** (124,235 records, 5 attributes):
   - `person_id`: Unique person identifier.
   - `id`: Unique title identifier linking back to `titles.csv`.
   - `name`: Full name of the credited talent.
   - `character`: Name of the fictional character portrayed (for actors).
   - `role`: Creative designation (`ACTOR` or `DIRECTOR`).

---

## 4. Technologies Used
* **Programming Language:** Python 3.11
* **Data Manipulation & Aggregation:** Pandas, NumPy
* **Data Visualization:** Matplotlib, Seaborn
* **Data Parsing:** `ast.literal_eval` (safe string-to-list parsing)
* **Development Environment:** Jupyter Notebook

---

## 5. Project Folder Structure
```text
Amazon-Prime-EDA/
│
├── datasets/
│   ├── titles.csv
│   └── credits.csv
│
├── notebooks/
│   └── Amazon_Prime_EDA.ipynb
│
├── visualizations/
│   ├── correlation_heatmap.png
│   ├── imdb_score_distribution.png
│   ├── movies_vs_tv_shows.png
│   ├── release_year_trends.png
│   ├── runtime_distribution.png
│   ├── top_actors.png
│   ├── top_directors.png
│   ├── top_genres.png
│   ├── top_popular_titles.png
│   ├── top_production_countries.png
│   └── tv_show_seasons.png
│
├── README.md
├── requirements.txt
└── .gitignore
```

---

## 6. Data Cleaning & Transformation
1. **Deduplication:**
   - Identified and removed 3 duplicate records in `titles.csv` (retaining 9,868 clean titles).
   - Removed 56 duplicate records in `credits.csv` (retaining 124,179 clean entries).
2. **Missing Value Management:**
   - Evaluated structural missing values: `seasons` is appropriately null for movies.
   - Preserved genuine missing values in `age_certification` and ratings without dropping entire rows needlessly.
3. **Data Type Casting:**
   - Explicitly converted numeric columns (`release_year`, `runtime`, `seasons`, `imdb_score`, `imdb_votes`, `tmdb_popularity`, `tmdb_score`) using `pd.to_numeric(..., errors='coerce')`.
4. **List Literal Parsing:**
   - Handled stringified lists in `genres` and `production_countries` using a robust `ast.literal_eval` parser to convert strings like `"['drama', 'comedy']"` into genuine Python lists.
5. **Safe Working Copies:**
   - Original raw CSVs were preserved in `datasets/` without modification; all cleaning and analysis was performed on memory copies.

---

## 7. Analyses Performed & Key Findings

| Analysis | Focus | Key Finding |
|---|---|---|
| **1. Movies vs TV Shows** | Catalog Distribution | Movies comprise **86.3% (8,514 titles)** and TV Shows represent **13.7% (1,354 titles)**. |
| **2. Release-Year Trends** | Historical Growth | Exponential surge post-2015, peaking between 2018–2021 during the peak streaming era. |
| **3. IMDb Scores** | Audience Ratings | Overall mean of **6.01/10**. TV shows achieve higher median scores (~7.1) compared to movies (~5.9). |
| **4. Runtimes** | Duration Patterns | Average movie runtime centers around **98.4 minutes**; TV episodes average **35–45 minutes**. |
| **5. TV Show Seasons** | Series Longevity | Over **67%** of series have only 1 season; multi-season renewals fall sharply (16% for 2 seasons). |
| **6. Top Genres** | Catalog Genre Strengths | **Drama** (4,764 titles), **Comedy** (2,987 titles), and **Thriller** (2,119 titles) lead all categories. |
| **7. Production Countries** | Geographical Reach | **United States** (5,334 titles) leads, followed prominently by **India** (1,072 titles) and the **United Kingdom** (928 titles). |
| **8. Popular Titles** | TMDB Popularity Index | Driven by major releases (*All the Old Knives*, *Harina*, *Hotel Transylvania*) and syndicated staples (*Suits*, *Better Call Saul*). |
| **9. Actor Analysis** | Prolific Talent | Led by classic western and Hollywood legends (**George 'Gabby' Hayes**, **Roy Rogers**) and Indian icons (**Nassar**). |
| **10. Director Analysis** | Prolific Directors | Prolific studio directors (**Joseph Kane**, **Sam Newfield**) and modern stand-up comedy directors (**Jay Chapman**). |
| **11. Dataset Merging** | Relational Integration | Left-joined 9,868 titles with 124,179 credits on `id` to produce 124,534 enriched title-credit records. |
| **12. Correlation Analysis** | Feature Relationships | Strong correlation (0.60) between IMDb and TMDB scores; no strong correlation between release recency and score. |

---

## 8. Visualizations Created
All plots were generated using Matplotlib and Seaborn, formatted with clean titles, labels, and legends, and saved to `visualizations/`:

- `movies_vs_tv_shows.png`: Bar chart and percentage pie chart of content distribution.
- `release_year_trends.png`: Multi-line historical progression of total titles, movies, and TV shows.
- `imdb_score_distribution.png`: Histogram with KDE curve and side-by-side boxplots by type.
- `runtime_distribution.png`: Distribution histogram and boxplot comparing movie vs episode duration.
- `tv_show_seasons.png`: Bar chart depicting the count and percentage of series season lengths.
- `top_genres.png`: Horizontal bar chart of the top 10 content genres.
- `top_production_countries.png`: Horizontal bar chart of the top 10 producing nations.
- `top_popular_titles.png`: Horizontal bar chart of the top 10 most popular titles by TMDB score.
- `top_actors.png`: Horizontal bar chart of the top 10 most credited actors.
- `top_directors.png`: Horizontal bar chart of the top 10 most credited directors.
- `correlation_heatmap.png`: Pearson correlation heatmap across 7 numerical attributes.

---

## 9. Installation and Setup

### Prerequisites
Make sure you have Python 3.9+ installed on your system.

### Step 1: Clone the Repository
```bash
git clone YOUR_GITHUB_REPOSITORY_URL
cd Amazon-Prime-EDA
```

### Step 2: Set Up Virtual Environment (Optional but Recommended)
```bash
python -m venv venv
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate
```

### Step 3: Install Required Dependencies
```bash
pip install -r requirements.txt
```

### Step 4: Launch Jupyter Notebook
```bash
jupyter notebook
```
Navigate to:
```text
notebooks/Amazon_Prime_EDA.ipynb
```
Select **Kernel -> Restart & Run All** to reproduce all computations, tables, and charts.

---

## 10. Conclusion and Future Scope

### Conclusion
This project provides a comprehensive overview of Amazon Prime's library composition and content trends. Through clean exploratory data analysis, we validated that Amazon Prime combines a massive catalog of films with focused TV offerings, leaning heavily on Drama and Comedy genres, with major regional focus on the United States and India.

### Future Scope
1. **Personalized Recommendation Engine:** Implement content-based filtering using cosine similarity on TF-IDF transformed genres, descriptions, and cast lists.
2. **Interactive Web Dashboard:** Build a dynamic frontend dashboard using **Streamlit** or **Dash** with interactive sliders for release year, ratings, and genre filters.
3. **Sentiment Analysis:** Collect viewer review text from Rotten Tomatoes or IMDb to perform sentiment classification and word clouds.
4. **Cross-Streaming Comparative EDA:** Merge datasets from Netflix, Disney+, Hulu, and Amazon Prime to compare catalog size, genre emphasis, and exclusivity.
