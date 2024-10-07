

## Exploratory Data Analysis (EDA) Report on Swiggy Restaurant Dataset

### 1. **Objective**
To conduct an in-depth exploratory data analysis (EDA) of the Swiggy restaurant dataset to uncover key insights about restaurant distribution, customer ratings, food types, pricing, and delivery times.

### 2. **Data Overview**
- **Total Rows**: 8680
- **Total Unique Restaurants**: 7865

#### **Dataset Structure**
| Column               | Description                                   |
|----------------------|-----------------------------------------------|
| ID                   | Unique identifier for each restaurant        |
| Area                 | Specific area of the restaurant              |
| City                 | City where the restaurant is located         |
| Restaurant           | Name of the restaurant                        |
| Price                | Price of the food item                       |
| Average_Ratings      | Average customer ratings                      |
| Total_Ratings        | Total customer ratings received               |
| Food_Type            | Type of food served by the restaurant        |
| Address              | Address of the restaurant                     |
| Delivery_Time        | Average time taken for delivery               |
| Rating_Category      | Categorization of ratings                     |

### 3. **Data Cleaning & Preparation**
- **Duplicate Checking**: 
  - Created a temporary table with distinct values; confirmed no duplicates in the dataset.
  
- **Column Renaming**: 
  - Standardized column names for consistency (e.g., `Delivery time` to `Delivery_Time`).

- **Null Value Checking**: 
  - No null values found across all critical columns.

- **Data Trimming**: 
  - Removed leading and trailing spaces from `CITY` and `RESTAURANT`.

- **New Column Addition**: 
  - Introduced `RATING_CATEGORY` based on `Average_Ratings` with categories: Poor, Average, Good, Excellent.

### 4. **Univariate Analysis**
- **Total Number of Restaurants**: 
  - Total: **8680**, Unique: **7865**
  
- **Restaurants by City**:
  ```sql
  SELECT CITY, COUNT(*) AS NO_OF_RESTAURANTS 
  FROM SWIGGY 
  GROUP BY CITY 
  ORDER BY NO_OF_RESTAURANTS DESC;
  ```
  - Highest: Hyderabad, followed by Chennai.

- **Top 5 Most Frequent Addresses**: 
  ```sql
  SELECT Address, COUNT(*) AS Frequency 
  FROM SWIGGY 
  GROUP BY Address 
  ORDER BY Frequency DESC LIMIT 5;
  ```
  
- **Average, Minimum, and Maximum Ratings**:
  - **Average Rating**: 3.66
  - **Minimum Rating**: 2
  - **Maximum Rating**: 5

- **Food Type Distribution**:
  ```sql
  SELECT FOOD_TYPE, COUNT(*) AS RESTAURANT_COUNT 
  FROM SWIGGY 
  GROUP BY FOOD_TYPE 
  ORDER BY RESTAURANT_COUNT DESC;
  ```

- **Price Distribution**:
  - **Average Price**: 348.44
  - **Minimum Price**: 0
  - **Maximum Price**: 2500

- **Delivery Time Statistics**:
  - **Average Delivery Time**: 53.97 mins
  - **Minimum Delivery Time**: 20 mins
  - **Maximum Delivery Time**: 109 mins

### 5. **Bivariate Analysis**
- **Average Rating by Food Type**:
  ```sql
  SELECT FOOD_TYPE, AVG(AVERAGE_RATINGS) AS AVG_RATING 
  FROM SWIGGY 
  GROUP BY FOOD_TYPE 
  ORDER BY AVG_RATING DESC;
  ```
  - Highest rated: Healthy Food, Salads.

- **Average Price by Food Type**:
  ```sql
  SELECT FOOD_TYPE, AVG(PRICE) AS AVG_PRICE 
  FROM SWIGGY 
  GROUP BY FOOD_TYPE 
  ORDER BY AVG_PRICE DESC;
  ```
  - Most expensive: Japanese, Korean.

- **Total Ratings by City**:
  ```sql
  SELECT CITY, SUM(TOTAL_RATINGS) AS TOTAL_SUM 
  FROM SWIGGY 
  GROUP BY CITY 
  ORDER BY TOTAL_SUM DESC;
  ```
  - Highest: Hyderabad.

- **Average Ratings vs. Total Ratings**:
  ```sql
  SELECT Average_Ratings, SUM(Total_Ratings) AS Total_Ratings 
  FROM SWIGGY 
  GROUP BY Average_Ratings 
  ORDER BY Average_Ratings;
  ```

- **Delivery Time Impact on Ratings**:
  ```sql
  SELECT DELIVERY_TIME, AVG(AVERAGE_RATINGS) AS AVG_RATING 
  FROM SWIGGY 
  GROUP BY DELIVERY_TIME 
  ORDER BY DELIVERY_TIME;
  ```

### 6. **Key Findings**
- **Distribution**: 
  - High concentration of restaurants in Hyderabad and Chennai.
  
- **Customer Satisfaction**: 
  - Majority rated as "Good" or "Excellent."
  
- **Operational Efficiency**: 
  - Majority of restaurants deliver within 30-60 minutes.

- **Food Type Insights**: 
  - Higher ratings for premium food types like "Healthy Food."

- **Price Trends**: 
  - Significant price variation across cities; Mumbai has the highest average price.

### 7. **Conclusion**
The exploratory analysis of the Swiggy dataset revealed several interesting patterns in restaurant distribution, customer ratings, and delivery performance.
Cities like Chennai show a higher restaurant quality, while Hyderabad is the most populous in terms of the number of restaurants and customer engagement. Delivery 
times remain a critical factor influencing customer satisfaction, and premium food types like Japanese and Barbecue cater to higher-end customers.

DATASET:Kaggle(Swiggy Restaurants dataset)
