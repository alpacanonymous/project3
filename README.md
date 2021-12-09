![kangaroos](https://github.com/aykim1127/project3/blob/main/images/kangaroos.jpeg)

# Predicting Rain Tomorrow in Australia
Authors: Angela Kim, Colin Pelzer, Daniel Burdeno, Steven Addison


## Overview
This project analyzes climate data of various locations in Australia and designs the best classification model to predict whether it will rain tomorrow based on different weather features such as relative humidity, cloud cover, and atmospheric pressure.


## Business Problem
Agriculture is an essential part of Australia's economy, and rainfall plays a big role in its success. Knowing whether it will rain tomorrow or not can help farmers make better decisions on how to tend to their crops. It's important to know what kinds of weather conditions (ie. relative humidity, hours of sunshine) will determine precipitation in order to implement the best methods to protect crops and secure a high and robust yield. For areas with low rainfall, it would be important to know if it will rain so that farmers know if they should prepare to water their crops or not. For areas with high rainfall, farmers can use a predictive model to protect their crops from flooding.


## Data Understanding
The data comes from the [Australian Government Bureau of Meteorology](http://www.bom.gov.au/climate/data/) and covers climate statistics from 2007-2017, which was then compiled into a dataset found on [Kaggle](https://www.kaggle.com/jsphyg/weather-dataset-rattle-package). We supplemented this dataset with data from other sources <a href="#Sources">(see below)</a>. This dataset covers 49 locations from all over Australia and contains records for 22 weather features with their corresponding dates. Refer [here](https://rdrr.io/cran/rattle.data/man/weatherAUS.html) for description about each feature. After exploring and preparing the data, we designed a classification model to predict whether it will "Rain Tomorrow" in the various locations in Australia.


## Data Preparation & Analysis
The `weatherAUS` dataset contains 145,460 entries(rows) with 343,248 null values. The target for our models is `RainTomorrow`. Nearly every feature(column) has null values with the exception of `Date` and `Location`. We were able to fill in the majority of missing values in `Sunshine` using data provided by [BOM](http://www.bom.gov.au). We did this by creating a nested dictionary of each location with the mean values of `Sunshine` for each month. We extracted `Month` from `Date` then used a for loop to replace a null value for `Sunshine` based on `Location` and `Month`. All other missing values were imputed using sklearn's KNNImputer. We dropped `Evaporation` because about 43% of its values were missing, and we couldn't find any information to fill them in. We removed the three records of 9 within the `Cloud9am` and `Cloud3pm` columns under the assumption that they were misrecorded because the values range from 0-8 [oktas](https://en.wikipedia.org/wiki/Okta). All categorical features were encoded using sklearn's OneHotEncoder.


## Modeling
We chose <i>accuracy</i> as our evaluation metric for our models because predicting rain accurately is the most valuable information for farmers. If they are expecting no rain in a drier region, they can prepare sprinklers. If they are expecting rain in a wetter region, they can protect their crops from flooding.

Baseline Model Accuracy Score: 0.668

Logistic Regression Accuracy Score: 0.787

Random Forest Accuracy Score: 0.843

Decision Tree Accuracy Score: 0.844

Gradient Boost Accuracy Score: 0.856

XGBoost Accuracy Score: 0.862


## Visualizations
![accuracy chart](https://github.com/aykim1127/project3/blob/main/images/accuracy_chart.png)


## Conclusions
TEXTY TEXT

To view our presentation, click [here](https://www.canva.com/design/DAEx3uG5NIU/PnQ6UHDDkNjACTbod4degQ/view#4).

## Next Steps
Because the dataset covers the entire continent of Australia, which includes a wide range of climates, our next step would be to make individual models for each of the 49 locations.


## <a id="Sources">Sources</a>
- [Dataset on Kaggle](https://www.kaggle.com/jsphyg/weather-dataset-rattle-package)
- [Australian Government Bureau of Meteorology](http://www.bom.gov.au/climate/data/)
- [Description & Format of weatherAUS dataset](https://rdrr.io/cran/rattle.data/man/weatherAUS.html)
- [Climate-Data.org](https://en.climate-data.org/oceania/australia-140/)
- [The Role of Weather and Weather Forecasting in Agriculture](https://www.dtn.com/the-role-of-weather-and-weather-forecasting-in-agriculture/)


## Repository Structure
```
├── data
│    ├── sunshine.py
│    ├── weatherAUS.csv
│    ├── X_test_KNNI.csv
│    ├── X_train_KNNI.csv
│    ├── y_test.csv
│    └── y_train.csv
├── .gitignore
├── images
├── README.md
├── slides.pdf
└── notebook.ipynb
```
