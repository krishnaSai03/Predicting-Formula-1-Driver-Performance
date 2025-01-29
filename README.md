# Predicting-Formula-1-Driver-Performance
Predicting Formula 1 Driver Performance: A Data-Driven Approach to Performance Insights
#### 1. Problem Statement 
The objective of this project is to predict Formula 1 drivers' race points, a critical indicator of 
performance and contribution to team standings, using historical data. This insight aids in assessing 
consistency, skill, and the potential for podium finishes. 
#### 2. Introduction 
Predicting driver points is crucial in assessing a driver’s performance and their contribution to the 
overall team standing in a Formula 1 season. Points directly reflect the consistency, skill, and 
competitiveness of a driver across races, which are key indicators of their ability to win 
championships or achieve podium finishes. By accurately forecasting points, teams and analysts 
can strategize better, optimize resource allocation, and gain insights into performance trends, 
which are valuable for both mid-season decisions and long-term planning. 
#### 3. Data Collection 
Source: The Ergast Motor Racing Data API provided comprehensive historical F1 data. 
Link: https://ergast.com/mrd/db/

#### Datasets Used: 
##### Results (results.csv): 
This dataset is the backbone of my analysis as it contains critical information about race 
outcomes, including positions, points, fastest laps, and status codes. These elements are 
directly tied to performance prediction. 
##### Status (status.csv): 
Understanding a driver's status during the race (e.g., finished, retired, or disqualified) is 
key for identifying patterns in DNFs (Did Not Finish) and reliability issues, which are 
significant factors in race outcomes. 
##### Drivers (drivers.csv): 
This dataset provides demographic and identity data, such as driver names, nationalities, 
and birthdates. These are essential for including driver-specific trends (e.g., experience, 
age) in my analysis. 
##### Races (races.csv): 
Race-specific metadata, like the circuit, season, and race date, adds context to the 
analysis. This helps in understanding how different tracks and years influence 
performance. 
##### Constructors (constructors.csv): 
Since Formula 1 is a team sport, constructor data helps capture the impact of team 
performance, technology, and reliability on race results.
##### Driver Standings (driver_standings.csv): 
This dataset adds longitudinal insights into a driver’s performance throughout the season, 
providing a benchmark for predictive modeling. 

By choosing these datasets, we ensured that our analysis covers the most impactful aspects of race 
performance while keeping the project focused and computationally efficient. Other datasets, like 
lap_times, pit_stops, or qualifying, were excluded because they are too granular and outside the 
scope of our goal, which emphasizes high-level race outcomes rather than specific intra-race 
dynamics."
#### 4.Data Preprocessing
##### Data Integration
##### Verification 
##### Missing Values 
##### Replacing the placeholder \N
##### Renaming  
##### Dropping the Unnecessary Columns

#### 5. Feature Engineering 
The feature engineering process begins by creating a new column for the full driver name by 
concatenating the driver_first_name and driver_last_name columns. This step simplifies the 
dataset by providing a single field to represent the driver's identity, enhancing readability and ease 
of use in analysis. Once the new driver_name column is created, the original driver_first_name 
and driver_last_name columns are removed to reduce redundancy and maintain a cleaner dataset.   
Next, the date-related columns, driver_date_of_birth and race_date, are converted to a datetime 
format to facilitate chronological calculations. Using these fields, the driver's age at the time of 
each race is calculated by finding the difference in days between the race date and the driver’s date 
of birth, then converting this difference into years. This derived feature, drivers_age_at_race, is 
rounded to make it more practical for analysis and modeling. After deriving the age feature, the 
original date columns are dropped as they are no longer needed, ensuring the dataset remains 
streamlined.  
The constructor names are updated to reflect their modern equivalents, aligning historical team 
data with current naming conventions. This is done through a series of conditional replacements, 
where outdated names like "Force India" and "Racing Point" are unified under "Aston Martin," 
and other names such as "Sauber" are updated to "Alfa Romeo." These transformations ensure 
consistency and improve the interpretability of the data, particularly when analyzing trends or 
performance over time for current constructors. By standardizing constructor names, the dataset 
becomes more cohesive and user-friendly for further analysis. 
##### Converting Lap Times 
Converting times to milliseconds allows for numerical comparisons and statistical analyses. 
Milliseconds format is better suited for machine learning models and mathematical operations. 
Dropping the original column reduces redundancy and maintains a clean dataset. 
#### 6. Exploratory Data Analysis (EDA) 
The chart below displays the distribution of unique drivers' ages at race time, showing a peak 
around 25-30 years, indicating that most drivers are in this age range during races. The distribution 
has a long right tail, suggesting fewer drivers compete at older ages (above 40). This highlights 
the concentration of drivers' careers during their younger years.   
![image](https://github.com/user-attachments/assets/10dadd7f-2c95-401b-921a-e9a522eb0c5a)

##### Distribution of Race Times
The plot shows the distribution of race times (in milliseconds) for unique races, with most race times clustering between 0.4e7 and 0.6e7 milliseconds. The distribution is slightly right skewed, indicating a few races with longer times. This analysis helps identify typical race durations and anomalies.  
![image](https://github.com/user-attachments/assets/68f883ed-4ad7-4602-b49f-3266acdcb0ba)
##### Top 10 Drivers by wins
The bar chart highlights the top 10 drivers by race wins, with Lewis Hamilton leading, followed by Michael Schumacher and Max Verstappen. The distribution shows a sharp decline in wins beyond the top three drivers. This analysis emphasizes dominance by a few drivers in Formula 1 history.  
![image](https://github.com/user-attachments/assets/dfb7f4bd-93a7-4498-ba74-00bf3d85cdae)
#### 7. Model Selection & Training
##### Importing Libraries:
•	Linear Regression, Random Forest Regressor, Decision Tree Regressor, and polynomial regression are imported for building regression models.
•	mean_squared_error and r2  score are used to evaluate the models' performance.
•	train_test_split is used to split the data into training and testing sets.
##### Splitting Data into Features and Target:
•	X contains the features (all columns except driver_points), which will be used to predict the target variable.
•	Y is the target variable, driver_points, which is continuous and will be predicted.
##### Splitting Data into Training and Testing Sets:
The data is split into training (80%) and testing (20%) sets using train_test_split.
•	random_state=42 ensures reproducibility of the split.
#### 8. Model Evaluation
##### 1. Linear Regression:
•	Mean Squared Error (MSE): 5.327 indicates relatively high prediction error compared to the other models.
•	R² Score: 0.7128 shows that the model explains about 71% of the variance in the target variable, which is decent but not the best performance among the models.
•	Evaluation: Linear Regression is limited in capturing nonlinear relationships, which may explain its relatively lower performance compared to other models.
##### 2. Random Forest:
•	MSE: 0.081, the lowest among all models, signifies minimal prediction error.
•	R² Score: 0.9956, near perfect, indicating that Random Forest explains almost all the variance in the target variable.
•	Evaluation: Random Forest performs exceptionally well, capturing complex patterns and providing accurate predictions. It is the best-performing model in this case.
![image](https://github.com/user-attachments/assets/fa6ce942-de9b-4752-b105-23367d9e3088)

##### 3. Decision Tree:
•	MSE: 0.228, slightly higher than Random Forest but significantly lower than Linear Regression.
•	R² Score: 0.9877, excellent performance, explaining nearly 99% of the variance.
•	Evaluation: Decision Tree performs well but is slightly less accurate than Random Forest. It may be prone to overfitting compared to ensemble methods like Random Forest.
##### 4. Polynomial Linear Regression:
•	R² Score: 0.9538, a significant improvement over basic Linear Regression, indicating that polynomial features help capture nonlinear relationships.
•	Evaluation: Polynomial Linear Regression effectively models nonlinearity but doesn’t match the performance of Random Forest or Decision Tree. Its slightly lower score might indicate overfitting to the training data.

#### 9. Insights and Interpretations
•	Key Predictors: Variables such as driver age, constructor points, and race time significantly influence driver points. Constructors with a history of strong performance consistently contribute to higher driver points.
•	Nonlinearity Captured: Polynomial features revealed that some relationships between variables and target outcomes are nonlinear, improving model performance.
•	Model Performance: Random Forest emerged as the most reliable model, with near-perfect R2 and minimal error, indicating its ability to handle complex, nonlinear relationships and interactions between variables.
•	Impact of Constructors: Updated constructor names (e.g., Force India → Aston Martin) reflected the importance of historical and contextual data alignment in model accuracy.
#### 10. Challenges Faced
•	Data Cleaning: Missing values were initially represented as strings ('\N'), requiring careful replacement with NaN for proper handling and imputation.
•	Feature Engineering: Creating meaningful features, such as driver age at race and converting lap times to milliseconds, demanded detailed domain knowledge and preprocessing effort.
•	High Dimensionality: The dataset included numerous features, requiring careful feature selection to reduce computational complexity without losing critical information.
•	Overfitting Risks: Complex models like Random Forest and Polynomial Regression required balancing accuracy with generalization to avoid overfitting.
#### 11. Conclusion and Recommendations
##### Conclusion: The project successfully identified key factors affecting F1 race outcomes and built a robust predictive model. Random Forest achieved the best performance, demonstrating its capability to model intricate relationships in the dataset.
##### Recommendations:
1.	Incorporating real-time race data to enhance model applicability for live predictions.
2.	Using ensemble methods like Gradient Boosting to explore further performance improvements.
3.	Expanding the dataset with additional variables, such as weather conditions and pit stop strategies, to capture more race dynamics.
4.	Continuously updating constructor and driver information to maintain model relevance.

#### 12. References
•	Formula 1 ERGAST Database (for historical race data) (https://ergast.com/mrd/)  
•	Pitwall Formula 1 Database (https://pitwall.app/ )  
•	https://wsb.wharton.upenn.edu/wp-content/uploads/2023/12/Padilla_2023_N.pdf   
•	https://www.researchgate.net/publication/368762920_Formula_One_Race_Analysis_Using_Machine_Learning  
•	Scikit-learn Documentation for machine learning techniques and preprocessing (https://scikit-learn.org/stable/ )  
•	Pandas and Matplotlib Documentation for data manipulation and visualization  






