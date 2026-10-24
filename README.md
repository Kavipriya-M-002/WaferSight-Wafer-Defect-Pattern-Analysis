# WaferSight: Wafer Defect Pattern Analysis

## Overview

WaferSight is an exploratory semiconductor wafer-map analysis project built using Python. It examines labelled wafer maps, calculates spatial defect metrics, visualizes defect patterns, and compares baseline machine-learning models for predicting wafer defect categories.

The project uses the first 10,000 rows of the WM-811K / LSWMD wafer-map dataset. From this subset, 410 wafers with known defect categories were used for the quantitative analysis and classification experiment.

**Project type:** Exploratory data analysis and baseline machine learning.

**Tools:** Python, Google Colab, NumPy, Pandas, Matplotlib, scikit-learn. 

**Application area:** Semiconductor wafer inspection and defect-pattern analysis.

## Objectives

- Explore wafer-map data and defect-category distributions.
- Visualize representative wafer maps.
- Calculate die counts and defect-rate measurements.
- Compare approximate center and edge defect statistics.
- Train and evaluate baseline classifiers.
- Document data-cleaning decisions and model limitations.

## Dataset

The project uses a 10,000-row subset taken from the beginning of the WM-811K / LSWMD dataset.

The wafer-map values follow the dataset's commonly used encoding:

- `0`: No die / background
- `1`: Normal die
- `2`: Defective die

Only wafers with known defect-category labels were included in the classification experiment.

### Dataset summary

| Item                     |  Value |
| ------------------------ | -----: |
| Rows inspected           | 10,000 |
| Labelled wafers analyzed |    410 |
| Defect categories        |      8 |
| Numerical input features |      7 |
| Training samples         |    328 |
| Test samples             |     82 |

The 410 labelled wafers are a subset of the first 10,000 rows, not a random or representative sample of the full dataset.

**Data access:** The original dataset is not included in this repository. Please consult the dataset's original publication or authorized source for access and usage terms.

## Methodology

### 1. Data loading and sampling

The original dataset was loaded in Google Colab using Google Drive storage. The first 10,000 rows were saved as a working sample to reduce repeated loading time.

### 2. Label processing

The nested failure-label representation was parsed to identify the actual category names. Wafers without known defect labels were excluded from the eight-category classification task.

### 3. Exploratory analysis

The analysis examined defect-category counts, wafer-map dimensions, stored values, and representative spatial patterns.

### 4. Quantitative wafer-map metrics

The following measurements were calculated for each labelled wafer:

- Valid die count
- Defective die count
- Defect rate
- Approximate center defect rate
- Approximate edge defect rate
- Center share of defective dies
- Edge share of defective dies

Defect rate is calculated as:

Defect rate (%) = Defective die count / Valid die count × 100

The center and edge measurements use a geometric approximation. They are exploratory metrics, not an industry-standard wafer-zone classification.

### 5. Data validation and correction

During development, a row-alignment problem was identified between the earlier Phase 3 metrics and the wafer labels. The metrics were recalculated directly from each wafer map while retaining its associated defect label.

The corrected metrics were then used to retrain and evaluate the models. Earlier evaluation scores were discarded in favor of the corrected results.

### 6. Machine-learning models

Two baseline classifiers were evaluated:

- Random Forest
- Logistic Regression

The data was split into training and testing subsets using an 80/20 stratified split with a fixed random seed. The models were evaluated on the same test set.

### 7. Evaluation metrics

The evaluation includes:

- Accuracy
- Balanced accuracy
- Macro F1-score
- Per-category precision, recall, and F1-score
- Confusion matrix
- Random Forest feature importance

## Results

### Model comparison

| Metric            | Random Forest | Logistic Regression |
| ----------------- | ------------: | ------------------: |
| Accuracy          |        57.32% |              39.02% |
| Balanced accuracy |        50.43% |              59.18% |
| Macro F1-score    |        0.4664 |              0.4737 |

Random Forest achieved higher overall accuracy. Logistic Regression achieved higher balanced accuracy and a slightly higher macro F1-score.

These results show a trade-off between overall correctness and performance across categories. Neither model is established as universally superior.

## Repository structure

```text
WaferSight-Wafer-Defect-Pattern-Analysis/
├── README.md
├── requirements.txt
├── .gitignore
├── notebooks/
│   └── Wafer_Defect_Analysis.ipynb
├── results/
    ├── figures/
    └── tables/
```

**Interests:** Semiconductor manufacturing, wafer inspection, metrology, process engineering, and data-driven defect analysis.

## Disclaimer

This is an educational and exploratory project for wafer-map analysis. It is not a validated semiconductor inspection system, and its results should not be interpreted as production-level defect-detection performance.
