# 🎬 Amazon Prime Movies and TV Shows – Exploratory Data Analysis (EDA) · v2.0

[![Python](https://img.shields.io/badge/Python-3.11-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![Pandas](https://img.shields.io/badge/Pandas-2.x-150458?style=for-the-badge&logo=pandas&logoColor=white)](https://pandas.pydata.org)
[![Seaborn](https://img.shields.io/badge/Seaborn-0.13-4c72b0?style=for-the-badge)](https://seaborn.pydata.org)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white)](https://jupyter.org)
[![GitHub Repo](https://img.shields.io/badge/GitHub-Repository-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/Pavan1720-git/Amazon-Prime-EDA)

A comprehensive, end-to-end Exploratory Data Analysis on **Amazon Prime Video's global catalog** of **9,868 titles** across **19 genres**, ratings, runtimes, production countries, and creative talent. Built with a sleek dark theme aesthetic and in-depth business intelligence insights.

---

## 📌 Table of Contents
1. [Project Overview](#-project-overview)
2. [Key Highlights & New in v2.0](#-key-highlights--new-in-v20)
3. [Dataset Schema](#-dataset-schema)
4. [Project Structure](#-project-structure)
5. [Data Cleaning Pipeline](#-data-cleaning-pipeline)
6. [Analyses & Key Findings](#-analyses--key-findings)
7. [Genre Spotlight & Best Picks](#-genre-spotlight--best-picks)
8. [Visualizations Gallery](#-visualizations-gallery)
9. [Installation & How to Run](#-installation--how-to-run)
10. [Executive Summary Table](#-executive-summary-table)
11. [Conclusion & Future Scope](#-conclusion--future-scope)

---

## 🎯 Project Overview
Amazon Prime Video is one of the world's premier streaming platforms, serving millions of global viewers with thousands of movies, television shows, and original productions. This project performs an exhaustive exploratory data analysis into the catalog to uncover strategic patterns in:
* **Content Composition:** Movies vs. TV Shows ratio and catalog architecture.
* **Historical Growth:** Era-by-era expansion from 1912 vintage cinema through the 2016–2022 streaming boom.
* **Genre Dynamics:** Deep breakdown of 19 genres including **Sci-Fi**, **Thriller**, **Romance**, **Horror**, **Action**, **Comedy**, and **Documentaries**.
* **Audience Reception:** IMDb scores, TMDB popularity metrics, and content quality tiers (Excellent to Poor).
* **Geographical Distribution:** Content production across 15+ nations led by the US, India, and the UK.
* **Creative Talent:** Prolific actors and directors shaping the Prime Video library.

---

## ✨ Key Highlights & New in v2.0
* 🎨 **Dark GitHub Aesthetic Theme:** All 12 visualization figures are custom-styled with dark backgrounds (`#0d1117`), cyan/gold accents, and high-contrast typography.
* 🎭 **Genre Deep Dive Across 19 Genres:** Exploded multi-genre lists to evaluate both volume and average audience satisfaction per genre.
* 🏆 **Curated Best Picks by Genre:** Top 3 highest-rated movies and shows for Thriller, Sci-Fi, Romance, Horror, Action, Comedy, Drama, Crime, and Animation.
* 🌟 **Quality Tier Classification:** Quantified catalog distribution across 5 tiers: *Excellent (8+)*, *Great (7–8)*, *Good (6–7)*, *Average (4–6)*, and *Poor (<4)*.
* ⏱️ **Runtime Categorization:** Feature films classified into Short, Standard, Feature, Long, and Epic categories.
* 🔗 **Relational Data Integration:** Joined `titles.csv` and `credits.csv` across 124,000+ cast records.

---

## 📂 Dataset Schema

### 1. `titles.csv` (9,871 raw records · 15 attributes)
| Column | Type | Description |
|---|---|---|
| `id` | `str` | Unique title identifier (e.g., `ts20945`, `tm19248`) |
| `title` | `str` | Name of the film or TV series |
| `type` | `str` | Content format: `MOVIE` or `SHOW` |
| `description` | `str` | Plot synopsis / storyline summary |
| `release_year`| `int64` | Year of initial release (1912 – 2022) |
| `age_certification` | `str` | Maturity rating (`R`, `PG-13`, `TV-MA`, `TV-14`, etc.) |
| `runtime` | `int64` | Total duration in minutes |
| `genres` | `str` | Stringified Python list of genres |
| `production_countries` | `str` | Stringified Python list of ISO country codes |
| `seasons` | `float64`| Number of seasons (populated for TV shows; null for movies) |
| `imdb_score` | `float64`| IMDb audience rating (scale 1.0 – 10.0) |
| `imdb_votes` | `float64`| Total user votes on IMDb |
| `tmdb_popularity` | `float64`| Rolling popularity index from TMDB |
| `tmdb_score` | `float64`| Average rating score on TMDB |

### 2. `credits.csv` (124,235 raw records · 5 attributes)
| Column | Type | Description |
|---|---|---|
| `person_id` | `int64` | Unique talent identifier |
| `id` | `str` | Title ID linking to `titles.csv` |
| `name` | `str` | Full name of actor or director |
| `character` | `str` | Character portrayed (for actors) |
| `role` | `str` | Creative credit: `ACTOR` (115,846) or `DIRECTOR` (8,389) |

---

## 📁 Project Structure
```text
Amazon-Prime-EDA/
│
├── datasets/
│   ├── titles.csv                 # Raw titles metadata (Preserved intact)
│   └── credits.csv                # Raw cast & crew metadata (Preserved intact)
│
├── notebooks/
│   └── Amazon_Prime_EDA.ipynb     # 54 cells: fully executed with dark theme outputs
│
├── visualizations/
│   ├── content_quality_tiers.png  # Overall & by-type quality tier breakdown
│   ├── correlation_heatmap.png    # Masked triangular Pearson correlation matrix
│   ├── imdb_score_distribution.png# Distribution KDE, violin plots, and quality bars
│   ├── movies_vs_tv_shows.png     # Donut chart & count bar chart
│   ├── release_year_trends.png    # Annual release progression & decade breakdown
│   ├── runtime_distribution.png   # Runtime histogram, category donut & boxplot
│   ├── top_actors.png             # Horizontal bar chart of top 15 actors
│   ├── top_directors.png          # Horizontal bar chart of top 15 directors
│   ├── top_genres.png             # Top 15 genres by count & average IMDb scores
│   ├── top_popular_titles.png     # Top 10 most popular titles with ratings
│   ├── top_production_countries.png# Top 15 countries & violin score distribution
│   └── tv_show_seasons.png        # Season count distribution & longevity donut
│
├── README.md                      # Comprehensive project documentation
├── requirements.txt               # Dependencies list
└── .gitignore                     # Configured for venv, checkpoints, and caches
```

---

## 🧹 Data Cleaning Pipeline
1. **Deduplication:**
   * Removed 3 duplicates from `titles.csv` $ightarrow$ **9,868 unique titles**.
   * Removed 56 duplicates from `credits.csv` $ightarrow$ **124,179 unique records**.
2. **Missing Value Preservation:**
   * Preserved `seasons` null values for movies without deletion (structural nulls).
   * Kept authentic nulls in `age_certification` and ratings without dropping entire rows.
3. **Safe Type Casting:**
   * Explicitly cast numeric columns using `pd.to_numeric(..., errors='coerce')`.
4. **List Parsing with AST:**
   * Handled stringified lists in `genres` and `production_countries` using `ast.literal_eval` with robust error guards.
5. **Feature Engineering:**
   * `decade`: Grouped into 10-year release intervals.
   * `quality_tier`: Classified into *Excellent*, *Great*, *Good*, *Average*, and *Poor*.
   * `runtime_cat`: Divided movie runtimes into *Short*, *Standard*, *Feature*, *Long*, and *Epic*.
   * `primary_genre`: Extracted the leading genre tag for each title.

---

## 📊 Analyses & Key Findings

| # | Analysis | Core Metric | Strategic Insight |
|---|---|---|---|
| **1** | **Movies vs. TV Shows** | 86.3% Movies vs. 13.7% TV Shows | Catalog is strongly oriented toward licensed feature films. |
| **2** | **Release Trends** | 60%+ content released after 2015 | Unprecedented content surge driven by the global streaming adoption boom. |
| **3** | **IMDb Scores** | Mean: 6.01 / 10 | TV shows achieve higher median ratings (~7.1) than movies (~5.9). |
| **4** | **Runtime Dynamics** | Movie mean: 98.4 minutes | 75% of movies fall between 60 and 120 minutes (Standard to Feature). |
| **5** | **TV Series Longevity** | 67.4% have only 1 season | High turnover of single-season / mini-series; sharp drop in renewals. |
| **6** | **Genre Landscape** | Drama leads count (4,764) | Documentaries score highest avg rating (6.99); Horror scores lowest (4.77). |
| **7** | **Geographic Hubs** | US: 5,334 \| India: 1,072 \| UK: 928 | India is Amazon Prime's fastest-growing international content hub. |
| **8** | **Popularity Ranking** | Top TMDB Popularity: 1,437.9 | High traffic for blockbusters (*All the Old Knives*, *Sonic*) & series (*Suits*). |
| **9** | **Genre Best Picks** | Curated Top 3 across 9 genres | Identifies hidden gems with ratings exceeding 9.0+. |
| **10**| **Quality Tiers** | 5% Excellent (8+) \| 41% Average | Vast catalog gives broad variety, with curated gems in upper tiers. |
| **11**| **Top Actors** | George 'Gabby' Hayes (49 titles) | Strong classic western archives & Indian cinema legends (Nassar: 37). |
| **12**| **Top Directors** | Joseph Kane (41 titles) | Prolific studio directors alongside comedy special directors (Jay Chapman: 34). |
| **13**| **Relational Merge** | 124,534 joined records | Unified dataset linking metadata with individual cast & crew credits. |
| **14**| **Correlation Analysis**| IMDb vs TMDB Score: +0.60 | High rating consistency across independent platforms. Release year does not dictate quality. |

---

## 🏆 Genre Spotlight & Best Picks

| Genre | Total Titles | Avg IMDb | Top Rated Title | Rating |
|---|---|---|---|---|
| **🔪 Thriller** | 2,119 | 5.54 | *Line of Duty* / *Shershaah* | **8.7** |
| **🚀 Sci-Fi** | 673 | 5.37 | *Fundamentally Cynical* / *The Boys* | **8.7 – 8.8** |
| **💕 Romance** | 1,752 | 6.02 | *Couple of Mirrors* / *Tom and Jerry* | **9.2 – 9.5** |
| **👻 Horror** | 1,065 | 4.77 | *Buzzfeed Unsolved* / *The Untamed* | **8.8** |
| **💥 Action** | 1,820 | 5.67 | *Pawankhind* / *Soorarai Pottru* | **9.2 – 9.9** |
| **😂 Comedy** | 2,987 | 5.99 | *Water Helps the Blood Run* / *Clarkson's Farm*| **9.1 – 9.7** |
| **🎭 Drama** | 4,764 | 6.13 | *Pawankhind* / *Jai Bhim* | **9.3 – 9.9** |
| **🔎 Crime** | 1,251 | 6.00 | *Jai Bhim* / *Couple of Mirrors* | **9.3 – 9.5** |
| **🎨 Animation** | 712 | 6.51 | *Bogyó és Babóca* / *The Long, Long Holiday* | **8.9 – 9.0** |
| **📹 Documentaries**| 1,096| **6.99** | *Surgeons: Edge of Life* / *Harmony with A.R. Rahman* | **9.1 – 9.2** |

---

## 🖼️ Visualizations Gallery
All 12 high-resolution visualizations are saved in [`visualizations/`](https://github.com/Pavan1720-git/Amazon-Prime-EDA/tree/main/visualizations):

* `movies_vs_tv_shows.png`: Donut chart of catalog ratio + count bar chart.
* `release_year_trends.png`: Annual release timeline (1970–2022) + decade bar chart + modern vs classic pie.
* `imdb_score_distribution.png`: Histogram with KDE curve, violin plots comparing Movies vs TV Shows, and quality tier breakdown.
* `runtime_distribution.png`: Distribution histogram, runtime category donut, and boxplots.
* `tv_show_seasons.png`: Bar chart of seasons distribution and series longevity classification.
* `top_genres.png`: Horizontal bar chart of top 15 genres by count and average IMDb rating comparison.
* `top_production_countries.png`: Horizontal bar chart of top 15 producing countries and violin plots for top 5.
* `top_popular_titles.png`: Horizontal bar chart of the top 10 most popular titles with release years and IMDb scores.
* `content_quality_tiers.png`: Donut chart of overall quality tiers and stacked bar chart by content type.
* `top_actors.png`: Horizontal bar chart of top 15 most featured actors with medal indicators.
* `top_directors.png`: Horizontal bar chart of top 15 most featured directors.
* `correlation_heatmap.png`: Triangular masked Pearson correlation heatmap across 7 numerical attributes.

---

## 💻 Installation & How to Run

### 1. Clone the Repository
```bash
git clone https://github.com/Pavan1720-git/Amazon-Prime-EDA.git
cd Amazon-Prime-EDA
```

### 2. Set Up Virtual Environment (Recommended)
```bash
python -m venv venv
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate
```

### 3. Install Dependencies
```bash
pip install -r requirements.txt
```

### 4. Launch Jupyter Notebook
```bash
jupyter notebook
```
Navigate to `notebooks/Amazon_Prime_EDA.ipynb`. All 54 cells are pre-executed with tables and dark-themed charts rendered.

---

## 📈 Executive Summary Table

| Metric | Calculated Value |
|---|---|
| **Total Titles Analyzed** | **9,868** |
| **Total Movies** | **8,514 (86.3%)** |
| **Total TV Shows** | **1,354 (13.7%)** |
| **Average IMDb Rating** | **6.01 / 10** |
| **Average Movie Runtime** | **98.4 minutes** |
| **Unique Genres Represented** | **19 genres** |
| **Most Popular Genre** | **Drama (4,764 titles)** |
| **Highest-Rated Genre** | **Documentation (avg 6.99 IMDb)** |
| **Top Production Country** | **United States (5,334 titles)** |
| **Second Production Country** | **India (1,072 titles)** |
| **Unique Actors Credited** | **68,131** |
| **Unique Directors Credited** | **4,888** |
| **Highest-Rated Title** | ***Pawankhind* (9.9 / 10)** |
| **Oldest Catalog Title** | ***The Champion* (1912)** |

---

## 🚀 Conclusion & Future Scope

### Conclusion
This project provides a comprehensive quantitative dissection of Amazon Prime Video's global entertainment catalog. The analysis proves that Amazon Prime leans heavily into feature films while curating acclaimed television series. Audience rating dynamics show that television viewers reward multi-episode storytelling with higher median ratings. Geographically, while the United States maintains the largest presence, India represents the platform's most vital international market.

### Future Scope
1. **Interactive Streamlit Web Dashboard:** Deploy a dynamic web app allowing live filtering by year, genre, and minimum IMDb score.
2. **Personalized Content Recommender:** Implement content-based cosine similarity on TF-IDF vectors derived from genres, plot synopses, and cast members.
3. **Sentiment Analysis on User Reviews:** Collect text reviews from IMDb/Rotten Tomatoes and apply NLP models for sentiment classification.
4. **Cross-Platform Benchmarking:** Merge Netflix, Disney+, and Amazon Prime datasets for a competitive multi-streaming platform comparative study.

---

<p align="center">
  <b>Amazon Prime Video EDA · Version 2.0</b><br>
  Developed by <a href="https://github.com/Pavan1720-git">Pavan Chaitanya</a>
</p>
