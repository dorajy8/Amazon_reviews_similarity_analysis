# Amazon Reviews Analysis

## Overview

This project investigates whether the rise of AI-generated content has contributed to redundant and fake product reviews on Amazon. Using two Amazon review datasets spanning **2000–2023** (285 months of data), the analysis applies scalable, similarity-based techniques to detect duplicate and near-duplicate reviews at scale.

**Core question:** Can big data methods detect AI-generated or duplicated reviews?

---

## Dataset

- **Source:** Two Amazon product review datasets, merged
- **Timeframe:** 2000–2023
- **Scope:** Multiple product categories including Beauty, Electronics, Cell Phones & Accessories, Automotive, Health & Personal Care, and Amazon Home

---

## Methodology

### Data Cleaning & Preprocessing
- Detected and removed ~1% duplicate records (filtered by timestamp + `user_id`)
- Removed columns with high null rates
- Dropped records missing critical fields: category, rating, product title, timestamps, or join keys
- Joined two datasets and retained only essential columns for analysis

### Exploratory Data Analysis (EDA)
- **Time series analysis** of review volumes (2000–2023), identifying COVID-era spikes (late 2019, early 2020, March–April 2021)
- **Top reviewed products:** Screen protectors, beauty tools, wireless chargers dominated review counts
- **Category analysis:** All Beauty, Cell Phones & Accessories, and Automotive had the highest review volumes, with distinct seasonal patterns
- **Rating distribution:** Most reviews clustered in the 4.0–4.5 range; very few products fall in the 0–2 range
- **Price vs. rating:** Higher-priced items received fewer but more consistently positive reviews
- **Sentiment word analysis:** Compared common words in 5-star vs. 1-star reviews; top reviewers wrote across many categories

### Similarity Detection via LSH (Locality-Sensitive Hashing)
- Applied **MinHashLSH** to detect near-duplicate reviews at scale
- Analyzed **8,058 review titles** and full review texts separately
- Compared recent reviews (2022–2023, n=5,103) vs. older reviews (pre-2022, n=5,061)

---

## Key Findings

| Finding | Detail |
|---|---|
| Title duplication rate | **45.45%** of reviews share similar titles |
| Text duplication rate | Only **7.40%** of review texts are similar |
| Recent vs. older reviews | Recent reviews show *lower* lexical duplication — likely because AI-generated text is lexically unique |
| Top reviewed products | Most highly-rated, highly-reviewed products are priced **under $25** |
| Category mislabeling | Products like "screen protectors" were found in the Amazon Fashion category |

**Key insight on AI:** LSH detects *lexical* duplication, not *semantic* similarity. AI-generated reviews tend to be uniquely worded, meaning they evade LSH detection — suggesting traditional duplicate-detection methods are insufficient for modern AI-generated content.

---

## Recommendations

1. **Differentiated detection for titles vs. texts** — Apply distinct thresholds and strategies given the large gap in duplication rates between these fields.
2. **Multi-dimensional review structure** — Introduce aspect-level scoring (e.g., quality, shipping, value) to encourage detailed, authentic reviews over generic text.
3. **Reviewer incentive programs** — Reward frequent, high-quality reviewers to increase authentic review volume and counter AI-generated content.

---

## Tools & Technologies

- **PySpark** — distributed data processing and similarity computation
- **MinHashLSH** — scalable near-duplicate detection
- **Big data cloud infrastructure** — UChicago cluster environment
- Python (pandas, matplotlib, wordcloud for EDA and visualization)

---

## Repository Structure

```
amazon-reviews-analysis/
├── data/               # Raw and cleaned datasets
├── notebooks/          # EDA and analysis notebooks
├── src/                # PySpark scripts (cleaning, LSH, analysis)
├── outputs/            # Charts, visualizations
└── README.md
```

---

## Author
**Dora Jiayue Li**  
MS Applied Data Science, University of Chicago  
Big Data and Cloud Computing (BDCP)
