# A Recipe for Success: A Data-Driven Exploration of Factors Influencing Restaurant Check-Ins on Yelp

## Project Overview

This study investigates the multifaceted factors influencing customer attendance at restaurants in Philadelphia, Pennsylvania, utilizing a rich dataset provided by Yelp. Recognizing that attendance is a crucial driver of revenue and profitability, this project aims to provide actionable insights for restaurant owners and investors seeking to optimize their business performance. Our analysis leverages Yelp’s extensive data repository, encompassing business attributes, images, customer reviews, star ratings, and crucially, check-in frequencies, which serve as a direct proxy for customer attendance.

The central hypothesis proposes that check-in frequency is influenced by a complex interplay of internal restaurant attributes, external competitive factors, and demographic factors.

## Key Findings

Our machine learning models, particularly the Neural Network (10, 10, 10) architecture, demonstrated strong predictive power for restaurant check-in frequency, achieving a Top Decile Lift (TDL) of 3.99, a Gini coefficient of 0.76, and an accuracy rate of approximately 89%.

The most influential variables identified through the models include:
*   `review_count`
*   `n_photo` (number of photos)
*   `attribute_count` (diversity of features/services)

## Business Recommendations

Based on the logistic regression analysis and overall model findings, here are key recommendations for Philadelphia restaurant owners and investors:

*   **Embrace Casual Dining:** Restaurants with a casual ambiance are significantly more likely to attract customers. Focus on creating a welcoming, relaxed, and comfortable atmosphere. Romantic, intimate, and upscale ambiances were not significant drivers of high check-in frequency.
*   **Maximize Visual Appeal:** A higher number of photos on a restaurant's Yelp profile is strongly associated with higher check-in frequency. Encourage customers to upload photos of the ambiance and food, and actively manage your restaurant's photo gallery.
*   **Offer Alcohol Service:** Restaurants serving alcohol (even just beer and wine) show significantly higher check-in frequencies. This caters to social dining experiences.
*   **Prioritize Credit Card Acceptance:** This remains a critical factor for customer convenience and attendance.
*   **Strategic Location with Demographics in Mind:** Restaurants in areas with higher concentrations of adults are more likely to have higher check-in frequencies. Tailor marketing and offerings to this demographic. Be mindful that high concentrations of children and elders showed a negative association with check-in frequency, suggesting different target markets might require different approaches.
*   **Consider Parking Solutions:** Offering a parking lot (not necessarily valet parking) can positively influence check-in frequency, especially in areas where street parking is limited.
*   **Online Reputation Management:** While star rating and review count had less influence compared to other factors in driving *high* check-ins, actively managing your online presence (responding to reviews, encouraging new ones) is still crucial for building trust and engagement.
*   **Reconsider Reservations & Delivery (Contextual):** The model suggested negative associations with `restaurantsreservations` and `restaurantsdelivery` regarding *high check-in frequency*. This might imply that for high volume, quick service is preferred, or that these features might attract a different customer segment not captured by the "high check-in" definition. Further investigation here is recommended based on specific business goals.

## Project Structure
```
├── README.md <- This file.
├── LICENSE <- License file (e.g., MIT License).
├── .gitignore <- Files/folders to be ignored by Git.
├── Term Paper <- Original term paper document.
├── Data/ <- Contains processed data used for analysis.
│ └── yelp_transformed_data.csv <- Transformed Yelp data, ready for R analysis.
├── Initial code/ <- Contains initial source code.
│ │ └── checkins_and_restaurant_success.ipynb <- Original Jupyter Notebook.
├── SQL code/ <- SQL queries for initial data extraction.
│ └── yelp_philadelphia_fastfood_analysis.sql.txt <- SQL scripts used in PgAdmin.
```
## Data Sources

The analysis relies on a rich dataset derived from Yelp's public dataset and external demographic information:

*   **Yelp Dataset:** A subset focusing on restaurant information, user reviews, and check-in data for Philadelphia, Pennsylvania, between January 1st, 2018, and December 31st, 2019. The raw Yelp dataset is very large and is not included in this repository.
*   **Demographic Data:** Population data (age group concentrations: youth, adults, elders, children) sourced from the 2018 American Community Survey Single-Year Estimates, provided by the U.S. Census Bureau. This data was merged with the Yelp data based on ZIP Code Tabulation Areas (ZCTA).

The `yelp_transformed_data.csv` file in `Data/` represents the aggregated and pre-processed dataset used as input for the R analysis.

## Methodology

The project followed a comprehensive data-driven methodology:

1.  **Data Acquisition & Initial Extraction:**
    *   Raw Yelp data was accessed.
    *   SQL queries (`SQL code/yelp_philadelphia_fastfood_analysis.sql`) were used in PgAdmin to extract relevant restaurant, review, and check-in information for Philadelphia and to perform initial joins.
    *   External demographic data was integrated.
2.  **Data Cleaning & Standardization:**
    *   Handling of missing values: "NA" marking for unmentioned attributes, dropping observations with zero reviews (to avoid distorted star ratings).
    *   Standardization of attributes to a 0-1 scale, with exceptions for categorical variables like `alcohol` and `wifi`.
    *   Imputation of `scaled_capped_business_proximity` using the `mice` method.
3.  **Exploratory Data Analysis (EDA):**
    *   Examination of multicollinearity using Variance Inflation Factor (VIF) and correlation plots.
    *   Analysis of demographic variable correlations and their implications for model inclusion.
    *   Assessment of data distributions (e.g., `check_in_count`) and transformations (log transformation).
4.  **Data Preprocessing for Machine Learning:**
    *   Binning of `check_in_count` into "High Range" and "Low Range" categories to define the target variable for classification.
    *   Addressing class imbalance using Synthetic Minority Over-sampling Technique (SMOTE).
    *   Min-Max Scaling applied to all attributes for optimal machine learning algorithm performance.
    *   Data split into training (75%) and evaluation (25%) sets.
5.  **Machine Learning Model Development & Evaluation:**
    *   Implemented and evaluated various classification algorithms: Logistic Regression, Naive Bayes, k-Nearest Neighbors (k-NN), Support Vector Machines (SVMs), Decision Trees, Bagging, Boosting, Random Forest, and Neural Networks.
    *   Model performance was assessed using Gini coefficient, Top Decile Lift (TDL), accuracy rate, and runtime.
    *   Hyperparameter tuning was performed, particularly for Neural Networks (various layer configurations) and k-NN (different 'k' values).
6.  **Results Interpretation & Business Recommendations:**
    *   Leveraged the insights from the best-performing models (Neural Network and Logistic Regression) to generate actionable business recommendations for restaurant owners and investors.

## Technologies Used

*   **R**: For data cleaning, preprocessing, exploratory data analysis, and machine learning model development.
    *   Key R Packages: `tidyverse` (for data manipulation: `dplyr`, `ggplot2`, etc.), `forcats` (for factor handling), `mice` (for imputation), `olsrr` (for regression diagnostics), `car` (for VIF), `psych` (for descriptive statistics), `nortest` (for normality tests), `lmboot` (for robust standard errors), `ggcorrplot` (for correlation visualization), `smotefamily` (for SMOTE), `doParallel` (for parallel processing), `caret` (for ML model training and evaluation), `naivebayes`, `kernlab` (for SVM), `NeuralNetTools`, `RSNNS` (for Neural Networks), `party`, `partykit` (for Decision Trees), `mboost` (for Boosting), `randomForest`.
*   **SQL (PostgreSQL/PgAdmin):** For initial data extraction and aggregation from the raw Yelp dataset.

## How to Run/Reproduce

To reproduce the analysis:

1.  **Clone the Repository:**
    ```bash
    git clone https://github.com/your-username/yelp-restaurant-checkins-philadelphia.git
    cd yelp-restaurant-checkins-philadelphia
    ```
2.  **Data Setup:**
    *   The `data/processed/yelp_transformed_data.csv` file is included in this repository as the direct input for the R script.
    *   **Note:** The original raw Yelp dataset is extremely large and not included. The SQL script `src/sql/yelp_philadelphia_fastfood_analysis.sql` demonstrates the queries used to extract relevant data from a PostgreSQL database (initialized with the Yelp JSON files). If you wish to work with the raw data directly, you would need to acquire the Yelp dataset (available here https://www.kaggle.com/datasets/yelp-dataset/yelp-dataset) and load it into a PostgreSQL database (e.g., via PgAdmin).
3.  **R Environment Setup:**
    *   Ensure you have R and RStudio (recommended) installed.
    *   Open `src/r/checkins_and_restaurant_success.R` (or the `.ipynb` notebook) in RStudio.
    *   **Install Required Packages:** Run the following commands in your R console to install all necessary libraries.
        ```R
        install.packages(c("forcats", "tidyverse", "dplyr", "mice", "olsrr", "car", "psych", "nortest", "lmboot", "ggcorrplot", "smotefamily", "doParallel", "caret", "naivebayes", "kernlab", "NeuralNetTools", "RSNNS", "party", "mboost", "randomForest", "import"))
        ```
4.  **Run the R Script:**
    *   Execute the `src/r/checkins_and_restaurant_success.R` script sequentially. The script loads the processed data, performs cleaning, preprocessing, and runs the machine learning models.
    *   If using the `.ipynb` notebook, open it in a Jupyter environment and run the cells.

## Future Work

*   **Expanded Feature Engineering:** Investigate the influence of additional restaurant attributes (e.g., specific cuisine types, historical check-in trends over longer periods, changes in ownership/management).
*   **Seasonality and Events:** Incorporate external factors like seasonal variations, local events, or weather conditions into the analysis to understand their impact on check-in frequency.
*   **Customer Segmentation:** Perform customer segmentation based on review content or user behavior to tailor recommendations more precisely.
*   **Revenue Prediction:** Explore modeling restaurant revenue or profitability directly, rather than just check-ins, to provide more direct financial insights.
*   **Geospatial Analysis:** Conduct more advanced geospatial analysis to understand neighborhood effects, transportation accessibility, and micro-location influences in greater detail.


## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
