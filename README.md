# 🍔 Unsupervised Clustering of Fast-Food Cheat Meals

An Unsupervised Machine Learning project that analyzes fast-food cheat
meals and discovers nutritional patterns using clustering algorithms.
The project groups meals into meaningful categories based on calories,
fats, carbohydrates, sugar, protein, sodium, and meal characteristics.

The primary objective is to identify different meal consumption patterns
without using predefined labels, and analyze how these clusters relate
to the workout effort required to burn off the meals.

## 🚀 Project Overview

This project applies unsupervised learning techniques to **8,000
fast-food orders** to discover natural nutritional groupings.

Three clustering algorithms are implemented and compared:

-   K-Means Clustering
-   Hierarchical (Agglomerative) Clustering
-   DBSCAN (Density-Based Spatial Clustering)

Principal Component Analysis (PCA) is also used to visualize the
discovered clusters in two dimensions.

After clustering, the results are compared with the existing
`workout_shock_tier` label to understand the relationship between meal
nutrition and workout effort.

## ✨ Key Features

-   📊 **Exploratory Data Analysis:** Analyzes nutritional distributions
    and feature correlations.
-   🧹 **Data Preprocessing:** Handles missing values, feature scaling,
    and categorical encoding.
-   🤖 **Multiple Clustering Algorithms:** Implements and compares three
    unsupervised learning techniques.
-   📈 **Optimal Cluster Selection:** Uses the Elbow Method and
    Silhouette Score.
-   🔍 **DBSCAN Hyperparameter Tuning:** Tests different epsilon and
    minimum sample configurations.
-   🎯 **Meal Segmentation:** Identifies moderate and heavy fast-food
    meal groups.
-   📉 **PCA Visualization:** Displays clusters using dimensionality
    reduction.
-   📋 **Model Evaluation:** Compares clustering performance using
    multiple internal evaluation metrics.
-   💾 **Result Export:** Saves trained models, cluster assignments,
    evaluation tables, and visualizations.

## 📂 Dataset Description

**Dataset:** Fast Food Cheat Meal and Workout Burn Dataset

  Property           Details
  ------------------ ---------------------------
  Total Records      8,000
  Total Columns      23
  Data Type          Numerical and Categorical
  Order Identifier   `order_id`
  Clustering Type    Unsupervised Learning

### Features Used for Clustering

A total of 10 meal-related features are selected.

**Categorical Features:** - `fast_food_chain` - `meal_category`

**Numerical Features:** - `item_count` - `total_calories` -
`fat_grams` - `saturated_fat_grams` - `carb_grams` - `sugar_grams` -
`protein_grams` - `sodium_mg`

**Important:** The `workout_shock_tier` column is excluded from the
clustering input and used only after clustering for external validation.
Consumer attributes such as body weight and fitness level are also
excluded.

## 🛠️ Technology Stack

  Category                   Technologies
  -------------------------- ---------------------------------
  Programming Language       Python
  Data Manipulation          Pandas, NumPy
  Machine Learning           Scikit-learn
  Data Visualization         Matplotlib, Seaborn
  Dimensionality Reduction   PCA
  Model Serialization        Joblib
  Development Environment    Jupyter Notebook / Google Colab

## ⚙️ Project Workflow

1.  **Data Loading:** Load the fast-food dataset and inspect records,
    data types, missing values, and duplicates.
2.  **Exploratory Data Analysis:** Generate nutritional distribution
    histograms and correlation heatmaps.
3.  **Feature Selection:** Select 10 meal-related features for
    clustering.
4.  **Preprocessing:** Apply median imputation and StandardScaler to
    numerical features, and most-frequent imputation and One-Hot
    Encoding to categorical features.
5.  **Optimal K Selection:** Evaluate K-Means for K = 2 to 10 using
    inertia and Silhouette Score.
6.  **Model Training:** Train K-Means, Hierarchical Clustering, and
    DBSCAN.
7.  **Hyperparameter Tuning:** Evaluate 27 DBSCAN configurations.
8.  **Cluster Interpretation:** Analyze nutritional characteristics of
    each cluster.
9.  **PCA Visualization:** Project the processed data into two principal
    components.
10. **Evaluation:** Compare algorithms using clustering evaluation
    metrics.
11. **Result Saving:** Export cluster assignments, trained models,
    tables, and plots.

## 🧠 Algorithms Implemented

### 1. K-Means Clustering

K-Means partitions the dataset into K clusters by minimizing the
within-cluster sum of squared distances.

-   Number of clusters: K = 2
-   Random state: 42
-   Initializations: 10

### 2. Hierarchical Clustering

Agglomerative Hierarchical Clustering groups similar records by
progressively merging clusters.

-   Number of clusters: 2
-   Linkage method: Ward

### 3. DBSCAN

DBSCAN identifies clusters based on density and can classify outliers as
noise.

Hyperparameters were tuned using: - Epsilon (`eps`): 0.5 to 3.0 -
Minimum samples: 5, 10, 15

Selected configuration: - `eps = 1.75` - `min_samples = 5`

## 📊 Model Evaluation

The algorithms are evaluated using three major clustering metrics.

-   **Silhouette Score:** Higher values indicate better cluster
    separation.
-   **Davies-Bouldin Index:** Lower values indicate better clustering.
-   **Calinski-Harabasz Score:** Higher values indicate better-defined
    clusters.

### Final Algorithm Comparison

  ------------------------------------------------------------------------------------------
  Algorithm          Clusters    Noise (%)   Silhouette   Davies-Bouldin   Calinski-Harabasz
                                                  Score                  
  -------------- ------------ ------------ ------------ ---------------- -------------------
  **K-Means**           **2**      **0.0**   **0.3467**       **1.1524**        **5,502.44**

  Hierarchical              2          0.0       0.2913           1.2587            4,717.51

  DBSCAN                   13          5.3       0.3428           1.2272               37.02
  ------------------------------------------------------------------------------------------

### Selected Model: K-Means

K-Means was selected as the final model because it achieved:

-   Highest Silhouette Score: **0.3467**
-   Lowest Davies-Bouldin Index: **1.1524**
-   Highest Calinski-Harabasz Score: **5,502.44**
-   100% record assignment without noise.

Although DBSCAN produced a high Silhouette Score of 0.6035 in one
configuration, it classified 99.4% of records as noise. Therefore, that
configuration was rejected.

## 🍟 Cluster Analysis

K-Means identified two major nutritional groups.

  Parameter            Moderate Meals     Heavy Meals
  ------------------ ---------------- ---------------
  Orders                5,275 (65.9%)   2,725 (34.1%)
  Average Calories       1,207.7 kcal    2,366.9 kcal
  Fat                          60.4 g         118.2 g
  Saturated Fat                24.0 g          47.4 g
  Carbohydrates               125.2 g         244.8 g
  Sugar                        46.6 g          92.6 g
  Protein                      41.3 g          78.7 g
  Sodium                   1,799.9 mg      3,560.4 mg

### Key Observations

-   Approximately 65.9% of orders belong to the moderate meal cluster.
-   Approximately 34.1% belong to the heavy meal cluster.
-   Heavy meals contain roughly twice the calories, fat, sugar, and
    sodium of moderate meals.
-   Both clusters have an average item count of 3.5.
-   Nutritional composition, rather than the number of ordered items, is
    the main factor separating the clusters.

## 🏋️ Workout Label Validation

After clustering, the discovered groups were compared with the existing
`workout_shock_tier` column.

  Workout Tier                     Moderate Cluster   Heavy Cluster
  ------------------------------ ------------------ ---------------
  Extreme / Half-Marathon Toll                15.7%           89.2%
  Severe Cardio Deficit                       40.5%           10.7%
  High Sweat Penalty                          40.2%            0.1%
  Moderate Burn                                3.6%            0.0%

The heavy meal cluster strongly corresponds to the Extreme /
Half-Marathon Toll category, demonstrating that nutritional information
alone can reveal patterns associated with workout effort.

## 📉 PCA Visualization

Principal Component Analysis (PCA) is applied to reduce the
23-dimensional processed dataset into two dimensions.

-   Principal Component 1 (PC1)
-   Principal Component 2 (PC2)

Together, these components explain **70.31% of the total variance**.

The resulting visualization helps understand how the two K-Means
clusters are distributed.

## 📁 Project Structure

``` text
Fast-Food-Cheat-Meal-Clustering/
│
├── Food_Analysis.ipynb
├── fast_food_cheat_meal_workout_burn.csv
│
├── outputs_unsupervised_clustering/
│   ├── feature_distributions.png
│   ├── correlation_heatmap.png
│   ├── elbow_method.png
│   ├── silhouette_by_k.png
│   ├── dbscan_neighbor_distances.png
│   ├── cluster_sizes.png
│   ├── pca_cluster_visualization.png
│   ├── three_algorithm_comparison.png
│   │
│   ├── kmeans_k_selection.csv
│   ├── dbscan_tuning_results.csv
│   ├── clustering_model_comparison.csv
│   ├── final_algorithm_comparison.csv
│   ├── final_cluster_profiles.csv
│   ├── cluster_vs_existing_label.csv
│   ├── final_cluster_assignments.csv
│   │
│   ├── preprocessor.joblib
│   ├── k_means_model.joblib
│   ├── hierarchical_clustering_model.joblib
│   ├── dbscan_model.joblib
│   │
│   ├── model_metadata.json
│   └── final_project_report.txt
│
└── README.md
```

*Note: The output folder is generated when the notebook is executed.
Actual filenames may vary slightly depending on the notebook execution
stage.*

## 💻 Installation and Execution

### 1. Clone the Repository

``` bash
git clone https://github.com/sairamareddy2/Fast-Food-Workout-Shock-Classification.git
```

### 2. Navigate to the Project Directory

``` bash
cd Fast-Food-Workout-Shock-Classification
```

### 3. Install Required Libraries

``` bash
pip install pandas numpy matplotlib seaborn scikit-learn joblib jupyter
```

### 4. Add the Dataset

Place the CSV file in the project directory:

``` text
fast_food_cheat_meal_workout_burn.csv
```

The notebook also supports the alternative filename
`fast_food_cheat_meal_workout_burn(1).csv`.

### 5. Run the Notebook

``` bash
jupyter notebook Food_Analysis.ipynb
```

Alternatively, upload the notebook and dataset to Google Colab and
execute the cells sequentially.

### 6. View Results

After successful execution, the generated plots, evaluation tables,
cluster assignments, and serialized models will be available in:

``` text
outputs_unsupervised_clustering/
```

## 📌 Applications

-   Fast-food nutritional pattern analysis.
-   Food consumption behavior segmentation.
-   Nutritional data exploration.
-   Meal intensity classification.
-   Fitness and workout-related data analysis.
-   Unsupervised learning research and experimentation.

## 🔮 Future Enhancements

-   Explore additional clusters for more detailed meal segmentation.
-   Perform clustering using nutritional features only.
-   Test Gaussian Mixture and Birch with the final feature set.
-   Perform cluster stability checks across different random seeds.
-   Develop an interactive dashboard using Streamlit.
-   Integrate personalized nutritional analysis and meal
    recommendations.

## ⚠️ Limitations

-   The dataset appears to be structured or synthetic; real-world
    generalization needs further testing.
-   Silhouette Scores are calculated using a sample of up to 2,000
    records.
-   One-hot encoding increases feature dimensionality and may affect
    distance-based clustering.
-   Internal clustering metrics measure geometric separation rather than
    real-world usefulness.

## 👨‍💻 Project Information

**Project Title:** Unsupervised Clustering of Fast-Food Cheat Meals

**Domain:** Machine Learning / Unsupervised Learning

**Techniques:** K-Means, Hierarchical Clustering, DBSCAN, PCA

**Dataset Size:** 8,000 Records

**Final Selected Algorithm:** K-Means (K = 2)

**Development Environment:** Python, Jupyter Notebook, Google Colab

------------------------------------------------------------------------

⭐ If you find this project useful, consider giving the repository a
star!
