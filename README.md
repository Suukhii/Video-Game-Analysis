# Video Game Sales Analysis & Global Sales Prediction

An exploratory data analysis and statistical learning project aimed at predicting worldwide video game sales prior to launch based on platform, genre, publisher, developer, ESRB rating, and metacritic review scores.

---

## Project Overview
Game studios invest millions of dollars into developing and marketing video games long before launch. Providing accurate pre-release global sales estimates allows publishers to optimize production budgets, allocate marketing resources effectively, and manage financial risk.

This project utilizes historical gaming data to build, evaluate, and compare multiple predictive regression models.

---

## Dataset & Variables

The dataset is sourced from Kaggle (**Video Games with Ratings**), compiled via web scraping from **VGChartz** and **Metacritic**. After filtering for complete cases across review fields, the dataset contains approximately **6,900 observations**.

The dataset is located in the parent directory as:
`../Video_Games_Sales_as_at_22_Dec_2016.csv`

### **1. Target Variable ($Y$)**
* `Global_Sales`: Total worldwide sales in millions of units.

### **2. Primary Predictors ($X$)** *(Known or estimated prior to/at launch)*
* `Platform`: Gaming hardware/console (e.g., PS4, X360, Wii, PC).
* `Genre`: Gameplay category (e.g., Action, Sports, Shooter, RPG).
* `Year_of_Release`: Year the game was released.
* `Publisher`: Distribution company (e.g., Nintendo, Electronic Arts, Activision).
* `Developer`: Studio responsible for creating the game.
* `Rating`: ESRB age rating (e.g., Everyone, Teen, Mature).
* `Critic_Score`: Aggregate review score compiled by Metacritic staff (0–100 scale).

### **3. Secondary Metadata & Regional Metrics**
* `Critic_Count`: Number of critics used for the `Critic_Score`.
* `User_Score`: Metacritic subscriber rating (0–10 scale).
* `User_Count`: Number of users who provided ratings.
* `NA_Sales`, `EU_Sales`, `JP_Sales`, `Other_Sales`: Regional sales breakdowns (excluded from prediction models to prevent data leakage).

---

## Exploratory Data Analysis

To evaluate whether critical reception correlates with commercial success prior to running statistical models, we examine the relationship between `Critic_Score` and `Global_Sales`:

![Scatterplot of Critic Score vs Global Sales](scatter_plot_critic_vs_sales.png)

### **Visualization Rationale**
A scatter plot with a fitted trendline was selected because both `Critic_Score` and `Global_Sales` are quantitative continuous variables. This visualization highlights:
* Overall linear and non-linear market trends.
* Heteroscedasticity (increased variance in sales at higher review scores).
* Extreme commercial outliers (blockbuster titles selling tens of millions of units).

---

## Analysis Plan & Methodology

1. **Data Preprocessing & Splitting:**
   * Clean and filter dataset to ~6,900 complete cases.
   * Split data into **Training**, **Validation**, and **Test** sets using **$K$-Fold Cross-Validation** to prevent overfitting.
2. **Baseline Modeling:**
   * Fit a **Multiple Linear Regression** model using all primary features.
3. **Feature Selection & Regularization:**
   * Apply **Stepwise Selection** and **Lasso Regression** ($L_1$ penalty) to select key features and remove noise from high-dimensional categorical variables.
4. **Non-Linear Extensions:**
   * Test **Polynomial Regression** and **Splines** to accurately model non-linear sales spikes observed among blockbuster games.
5. **Model Evaluation:**
   * Measure performance on unseen test data using **Mean Squared Error (MSE)** and **R-squared ($R^2$)**.

---

## How to Run

1. **Clone the Repository:**
   ```bash
   git clone [https://github.com/Suukhii/Video-Game-Analysis.git](https://github.com/Suukhii/Video-Game-Analysis.git)
   cd Video-Game-Analysis
