# Chicago Traffic Collision Analysis

## Project Overview
This project analyzes traffic crash data for Chicago from March 2013 to April 2024 to predict crash severity in terms of injuries and identify factors that have the highest impact on injury outcomes. Chicago, one of the largest US cities with over 6,400 km of roads spread across 600 km², experiences significant traffic congestion and this dataset contains information for more than 800,000 crashes.

## Problem Statement
Given that a crash has occurred, what is the expected crash severity in terms of injury? Moreover, which factors have the highest impact on injury expectations?
- Time
- Location
- Weather
- Road conditions
- Lighting conditions
- Posted speed limit

## Dataset Sources
- **Traffic Crashes**: Motor Vehicle Collisions crash table containing details on crash events from police reported motor vehicle collisions in Chicago. [Source](https://catalog.data.gov/dataset/traffic-crashes-crashes)
- **TIGER/Line Shapefiles**: Geospatial dataset containing ZIP code boundaries in the United States as per 2023 census. [Source](https://www.census.gov/geographies/mapping-files/time-series/geo/tiger-line-file.html)

## Exploratory Data Analysis
The dataset contains 817,841 crash records, each defined by 49 features grouped into:
- Road features
- Traffic features
- Surroundings features
- Crash features
- Police features
- Location features
- Outcome features

Key insights from EDA include:
- 8 ZIP codes account for 27.30% of total injuries, 36.64% of fatalities, and 26.51% of incapacitating injuries
- Top 15 streets own 33.95% of fatalities, with Halsted Street having the highest injury and fatality rate
- Fixed object collisions and pedestrian accidents account for 48.40% of fatalities
- 87.9% of accidents happened under good lighting conditions
- Most crashes occur in clear weather on dry roads

## Feature Engineering
- **ZIP Code Groups**: Created 4 ZIP code groups (A, B, C, D) based on fatality percentages to reduce dimensionality
- **Injury Class**: Created a simplified classification (A: Fatal injuries, B: Incapacitating injuries, C: Non-incapacitating injuries, D: No injuries)
- **Crash Hour Period**: Simplified 24 hours into 4 periods (Morning, Afternoon, Evening, Night)
- **Text Clustering**: Applied K-Means clustering to primary contributory causes to reduce their dimensionality

## Methodology
### Data Preparation
Special attention was given to balancing the dataset, as classes A and B (fatal and incapacitating injuries) constitute only 1.8% of the overall dataset.

### Models Developed
1. **Decision Tree Classifier** (Full and Reduced models)
   - Multi-class classification to classify data into 4 injury classes
   - Parameters: Gini impurity, max depth of 4

2. **Logistic Regression** (Full, Reduced, and Feature Enhanced models)
   - Binary classification (serious injury vs. non-serious injury)
   - Various regularization strengths tested

3. **Random Forest Ensemble**
   - 20 trees with max depth of 20
   - Feature importance based selection

## Evaluation and Results
Model performance comparison:

| Model | Accuracy | F1 Score |
|-------|----------|----------|
| Decision Tree (Full) | 85.72 | 85.72 |
| Decision Tree (Reduced) | 85.72 | 85.72 |
| Logistic Regression (Full) | 95.63 | 95.63 |
| Logistic Regression (Reduced) | 95.63 | 95.63 |
| Logistic Regression (Enhanced) | 93.20 | 93.20 |
| Random Forest (Reduced) | 93.47 | 93.47 |

The unbalanced nature of the dataset (98% negative, 2% positive cases) affected model performance for predicting injuries. A balanced model with equal representation showed better performance in predicting serious injuries.

## Key Findings
- Fixed object collisions and pedestrian accidents account for nearly half of all fatalities
- Certain ZIP code areas show significantly higher rates of serious injuries
- Most accidents occur in good weather and lighting conditions, suggesting human factors play a significant role

## Future Work
- **Balancing the Dataset**: Apply appropriate techniques to handle class imbalance
- **Time-series Prediction**: Explore time-series models such as GARCH
- **Additional Data Collection**: Incorporate population density, traffic congestion rate, and average traffic speed data

## Team Information
This project was developed by Team 60 for ISyE6740 – Course Project:
- Geeyavudeen Musthafa (gmusthafa3@gatech.edu)
- Mohammed Al-Desouky (ma@gatech.edu)

## Technologies Used
- Python
- NumPy
- Pandas
- Scikit-learn
- Matplotlib
- PyODBC (for database connections)

## How to Run
1. Clone this repository
2. Install required dependencies: `pip install -r requirements.txt`
3. Open `isye6740-project-model.ipynb` in Jupyter Notebook or JupyterLab
4. Execute the notebook cells sequentially

## References
1. Hertz, "Chicago Driving Guide," [Online]. Available: https://www.hertz.com/us/en/blog/planning-a-trip/chicago-driving-guide
2. "Chicago Leads Nation in 2022 Traffic Congestion," [Online]. Available: https://chicago.suntimes.com/2023/1/11/23550990/chicago-leads-nation-in-2022-traffic-congestion-report-says
3. "Chicago Data Portal - Traffic Crashes - Crashes," [Online]. Available: https://data.cityofchicago.org/Transportation/Traffic-Crashes-Crashes/85ca-t3if/about_data