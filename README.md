# Amazon Reviews Analytics & Suspicious Review Detection

**Course team project | Python · PySpark · NLP · Machine Learning · Data Visualization**

## Overview
This project explores Amazon customer review data and develops a **six-layer, heuristic approach to flag potentially suspicious review behavior**. The notebooks cover data preparation, exploratory analysis, sentiment and semantic analysis, and suspicious-review signals. Flags are **not verified fraud labels**, and the project does not establish supervised fraud-classification accuracy.

## Repository guide
| Notebook | Scope |
|---|---|
| [`01_data_preparation.ipynb`](notebooks/01_data_preparation.ipynb) | Read and join Parquet review/metadata inputs, clean data, and export a cleaned dataset. |
| [`02_reviews_eda_sentiment.ipynb`](notebooks/02_reviews_eda_sentiment.ipynb) | Analyze review ratings, sentiment distribution, rating/sentiment relationships, and temporal trends using PySpark, Pandas, and visualizations. |
| [`03_electronics_semantic_analysis.ipynb`](notebooks/03_electronics_semantic_analysis.ipynb) | Explore electronics review text with sentence embeddings (`all-MiniLM-L6-v2`), TextBlob sentiment, TF-IDF, and visualizations. |
| [`04_suspicious_review_detection.ipynb`](notebooks/04_suspicious_review_detection.ipynb) | Explore six suspicious-review signals and construct heuristic trust scores. |

## Analytical workflow
1. **Data preparation:** Load Parquet review and item data; clean and join records in PySpark.
2. **EDA and NLP:** Examine ratings, review text, sentiment trends, and semantic patterns.
3. **Suspicious behavior detection:**
   - **Layer 1:** User-behavior clustering with K-Means and PCA visualizations.
   - **Layer 2:** VADER sentiment versus star-rating mismatch.
   - **Layer 3:** Within-user review text similarity using TF-IDF.
   - **Layer 4:** Unusual bursts of reviews by product and date.
   - **Layer 5:** Product rating-distribution entropy.
   - **Layer 6:** Composite heuristic user/review trust index.
4. **Exploratory evaluation:** Review cluster silhouette scores, signal counts, and trust-level distributions. These are descriptive diagnostics, **not precision/recall or ground-truth fraud accuracy**.

## Recorded results
The following are **historical notebook outputs**, not a fresh rerun. Different layers use different samples and denominators.

| Metric | Recorded value | Interpretation |
|---|---:|---|
| Cleaned reviews | 1,978,436 | Data-preparation notebook verification |
| Unique users | 1,741,238 | Full review dataset |
| Active users in clustering | 38,326 | Subset used for user clustering |
| Selected K-Means clusters | 9 | Chosen using silhouette comparison |
| Silhouette score | 0.5153 | Clustering separation metric, not fraud accuracy |
| Users in suspicious clusters | 1,396 (3.64%) | Of clustered active users |
| Reviews sampled for sentiment | 594,477 | 30% review sample |
| Sentiment–rating mismatches flagged | 28,390 (4.78%) | Of sentiment sample |
| Users assessed for text similarity | 3,884 | Sample for TF-IDF analysis |
| Users with high text similarity | 78 (2.01%) | Similarity threshold > 0.5 |
| Products with review-burst patterns | 1,616 | Temporal anomaly signal |
| Products with suspicious rating entropy | 1,965 | Of 34,893 analyzed products |
| Low-trust reviews (heuristic) | 92,037 (4.7%) | Trust-tier output; not confirmed fake reviews |

**Caution:** The notebook's final summary also reports a mean trust score of 0.755, while a separate evaluation output lists lower trust-score percentiles. These summaries may use different aggregations or stages and should be reconciled before reporting a mean trust score externally. No ground-truth validation dataset is included in the provided notebooks.

## Tools and libraries
- **Processing:** Python, PySpark, Spark SQL, Pandas, NumPy, Parquet
- **NLP:** Hugging Face Transformers sentiment pipeline, VADER, TextBlob, Sentence Transformers, TF-IDF
- **ML and analysis:** Spark MLlib K-Means, PCA, silhouette scoring, scikit-learn
- **Visualization:** Matplotlib, Seaborn, word clouds
- **Environment:** Google Colab / Google Drive (original workflow)

## Reproducing the work
The notebooks are preserved as **course-project code** rather than a fully packaged, one-command pipeline. They reference Colab paths such as `/content/drive/MyDrive/reviews_cleaned.parquet` and intermediate Parquet files that are **not included** in this repository. Obtain the appropriate review and item datasets and update the paths in each notebook before running them. Run notebooks in the order shown above, allowing for separate exploratory branches in notebooks 02 and 03. The original environment may require additional version-specific packages and Colab setup.

**Privacy and upload note:** Original saved notebook outputs have been removed from the public-ready copies to avoid publishing raw review/user records, local runtime artifacts, or potentially identifying data. The historical aggregate metrics above were transcribed from the original notebook outputs. Do not upload raw Parquet, CSV exports containing user identifiers or review text, credentials, or Drive mounts without reviewing their provenance and sharing permissions.

## Limitations
- Suspicious behavior flags are heuristic indicators, **not proof of fraudulent activity**.
- Some layers use samples rather than the entire dataset; layer percentages should not be directly compared as if they shared the same denominator.
- The notebooks have not been rerun in a clean environment for this repository release.
- This was a **team course project**. Individual ownership and contributions should be documented after verification with the team/project report.

## Future improvements
- Rebuild a reproducible data-download and preprocessing pipeline.
- Add labeled review data and evaluate precision, recall, F1, and false-positive rates.
- Calibrate thresholds and composite trust scores; add ablation studies.
- Publish vetted aggregate visualizations and a concise findings report.

## Attribution
Course team project. Contributors and dataset citations to be confirmed from the original report or course materials before public release.
