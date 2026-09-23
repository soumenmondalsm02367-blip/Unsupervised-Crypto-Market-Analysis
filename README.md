# Unsupervised Learning for Cryptocurrency Market Analysis

**Presented by:** Soumen Mondal\
**Roll No.:** 35530824078\
**Registration No.:** 243550120261\
**Department:** CSE (AI & ML)\
**Year / Semester:** 3rd Year / 2nd Semester\
**Academic Year:** 2025--26

## Project Overview

This project applies **unsupervised machine learning** techniques to
cryptocurrency market data from Solana.

The project uses the actual `Solana_Price_data.csv` dataset containing
**1,368 observations** and the following market features:

-   Open
-   High
-   Low
-   Close
-   Volume

Three unsupervised-learning algorithms are implemented:

1.  **K-Means Clustering** --- groups similar market observations into
    three clusters.
2.  **DBSCAN** --- performs density-based clustering and identifies
    noise/outlier observations.
3.  **RBM (Restricted Boltzmann Machine)** --- learns two hidden
    features from the market data.

The final processed dataset contains the original features together with
the K-Means cluster, DBSCAN cluster, and RBM hidden-feature outputs.

## Dataset

### Dataset File

[Download / View Solana Price Dataset](Solana_Price_data.csv)

**Dataset name:** `Solana_Price_data.csv`

**Number of records:** 1,368

**Columns:**

  Column     Description
  ---------- ----------------
  `time`     Trading date
  `Open`     Opening price
  `High`     Highest price
  `Low`      Lowest price
  `Close`    Closing price
  `Volume`   Trading volume

The `time` column is used as the date/reference field. The five
numerical columns (`Open`, `High`, `Low`, `Close`, `Volume`) are used as
machine-learning features.

## Project Workflow

``` text
Solana_Price_data.csv
        |
        v
Data Loading
        |
        v
Feature Selection
(Open, High, Low, Close, Volume)
        |
        v
Preprocessing
        |
   +----+----+
   |         |
   v         v
StandardScaler   MinMaxScaler
   |         |
   |         v
   |        RBM
   |         |
   |       Hidden1
   |       Hidden2
   |
   +-------------------+
   |                   |
   v                   v
K-Means              DBSCAN
   |                   |
   v                   v
3 Clusters        Outlier Detection
   |                   |
   +---------+---------+
             |
             v
      Final Results CSV
```

## Technologies Used

### Programming Language

-   **Python**

### Libraries

-   **Pandas** --- loading and manipulating the CSV dataset
-   **Matplotlib** --- creating visualizations
-   **Scikit-learn** --- preprocessing, K-Means, DBSCAN, and RBM

### Machine Learning Algorithms

  Algorithm   Purpose
  ----------- ------------------------------------------------
  K-Means     Market clustering
  DBSCAN      Density-based clustering and outlier detection
  RBM         Hidden feature learning

## Preprocessing

Because the five numerical features have different scales, preprocessing
is applied before the algorithms.

### StandardScaler

`StandardScaler` is used for:

-   K-Means
-   DBSCAN

### MinMaxScaler

`MinMaxScaler` is used before:

-   RBM

## Algorithm Configuration

### K-Means

``` python
KMeans(
    n_clusters=3,
    random_state=42,
    n_init=10
)
```

### DBSCAN

``` python
DBSCAN(
    eps=0.9,
    min_samples=2
)
```

A DBSCAN label of `-1` represents a noise/outlier observation.

### RBM

``` python
BernoulliRBM(
    n_components=2,
    learning_rate=0.01,
    n_iter=300,
    random_state=42
)
```

The RBM generates:

-   `Hidden1`
-   `Hidden2`

## Project Results

### K-Means

K-Means produces **three clusters** from the Solana market observations.

The cluster labels are numerical group identifiers. They should not
automatically be interpreted as specific financial states without
additional analysis.

### DBSCAN

DBSCAN identifies dense regions and observations classified as noise
using the selected parameters.

-   `-1` = outlier/noise

### RBM

RBM learns a two-dimensional hidden representation:

``` text
Original Features
       |
       v
      RBM
       |
   +---+---+
   |       |
Hidden1  Hidden2
```

This provides a reduced hidden representation of the original market
features.

## Output File

The project generates:

[Solana ML Results](Solana_ML_Results.csv)

The output contains:

-   `time`
-   `Open`
-   `High`
-   `Low`
-   `Close`
-   `Volume`
-   `KMeans_Cluster`
-   `DBSCAN_Cluster`
-   `Hidden1`
-   `Hidden2`

## Project Files

A recommended project structure is:

``` text
Cryptocurrency-Market-Analysis/
│
├── Solana_Price_data.csv
├── Solana_ML_Results.csv
├── requirements.txt
├── main.py
├── README.md
└── Unsupervised_Learning_Cryptocurrency_Project_Report.docx
```

## Requirements

The project dependencies are listed in:

[requirements.txt](requirements.txt)

Contents:

``` text
pandas
matplotlib
scikit-learn
```

## Setup and Run Instructions

### 1. Download or clone the project

Keep all project files in the same folder.

### 2. Install the required libraries

Use the project's `requirements.txt` file to install the dependencies.

``` bash
pip install -r requirements.txt
```

### 3. Make sure the dataset is available

Place:

``` text
Solana_Price_data.csv
```

in the same directory as the Python program.

### 4. Run the Python project

The code can be run using:

-   Jupyter Notebook
-   JupyterLab
-   VS Code
-   Python IDE

### 5. Generated result

After execution, the processed dataset is saved as:

``` text
Solana_ML_Results.csv
```

## Visualizations

The project produces visualizations for:

1.  Solana closing-price trend
2.  K-Means clustering
3.  DBSCAN outlier detection
4.  RBM hidden-feature representation

## Key Information

-   **Learning type:** Unsupervised Learning
-   **Dataset:** Solana cryptocurrency market data
-   **Records:** 1,368
-   **Input features:** 5
-   **K-Means clusters:** 3
-   **DBSCAN:** Density-based clustering and noise detection
-   **RBM hidden features:** 2
-   **Final output:** `Solana_ML_Results.csv`

## Limitations

-   K-Means results depend on the selected number of clusters.
-   DBSCAN results depend on `eps` and `min_samples`.
-   Cluster labels are group identifiers and do not automatically
    represent bullish, bearish, or stable market states.
-   RBM hidden features are learned representations and may not have a
    direct financial interpretation.
-   The project is intended for exploratory analysis and does not
    guarantee future cryptocurrency price behavior.

## Future Scope

Possible extensions include:

-   Parameter tuning for K-Means and DBSCAN
-   Silhouette-score-based cluster evaluation
-   Additional cryptocurrency market features
-   Technical indicators such as returns and volatility
-   Comparison with hierarchical clustering and other unsupervised
    algorithms
-   Comparison of RBM with autoencoders
-   Interactive visualization/dashboard
-   Analysis across different time periods

## Conclusion

This project demonstrates an end-to-end unsupervised-learning workflow
for Solana cryptocurrency market analysis. K-Means is used for
clustering, DBSCAN for density-based outlier detection, and RBM for
hidden feature learning. The outputs from all three algorithms are
combined with the original dataset and saved in `Solana_ML_Results.csv`.

## References

-   Project presentation: *Unsupervised Learning for Cryptocurrency
    Market Analysis*
-   `Solana_Price_data.csv` --- project dataset
-   Scikit-learn documentation
-   Pandas documentation
-   Matplotlib documentation
