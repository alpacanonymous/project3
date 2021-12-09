![image](https://user-images.githubusercontent.com/79756630/145095351-9a4b9850-53b3-4f25-b3df-a4f471e03856.png)

# Predicting Rain Tomorrow in Australia
Authors: Angela Kim, Colin Pelzer, Daniel Burdeno, Steven Addison


## Overview
This project analyzes climate data of various locations in Australia and designs the best classification model to predict whether it will rain tomorrow based on different weather features such as relative humidity, cloud cover, and atmospheric pressure.


## Business Problem
Agriculture is an essential part of Australia's economy, and rainfall plays a big role in its success. Knowing whether it will rain tomorrow or not can help farmers make better decisions on how to tend to their crops. It's important to know what kinds of weather conditions (ie. relative humidity, hours of sunshine) will determine precipitation in order to implement the best methods to protect crops and secure a high and robust yield. For areas with low rainfall, it would be important to know if it will rain so that farmers know if they should prepare to water their crops or not. For areas with high rainfall, farmers can use a predictive model to protect their crops from flooding.


## Data Understanding
The data comes from the [Australian Government Bureau of Meteorology](http://www.bom.gov.au/climate/data/) and covers climate statistics from 2007-2017, which was then compiled into a dataset found on [Kaggle](https://www.kaggle.com/jsphyg/weather-dataset-rattle-package). We supplemented this dataset with data from other sources <a href="#Sources">(see below)</a>. This dataset covers 49 locations from all over Australia and contains records for 22 weather features with their corresponding dates. Refer [here](https://rdrr.io/cran/rattle.data/man/weatherAUS.html) for description about each feature. After exploring and preparing the data, we designed a classification model to predict whether it will "Rain Tomorrow" in the various locations in Australia.


## Data Preparation & Analysis
The `weatherAUS` dataset contains 145,460 entries(rows) with 343,248 null values. Nearly every feature(column) has null values with the exception of `Date` and `Location`. We were able to fill in the majority of missing values in `Sunshine` by taking the mean value for each month in each location provided by the [BOM](http://www.bom.gov.au). All other missing values were imputed using sklearn's KNNImputer. We dropped `Evaporation` because about 43% of its values were missing, and we couldn't find any information to fill them in. The target for our models is `RainTomorrow`.


## Modeling
We chose <i>accuracy</i> as our evaluation metric for our models because predicting rain accurately is the most valuable information for farmers. If they are expecting no rain in a drier region, they can prepare sprinklers. If they are are expecting rain in a wetter region, they can protect their crops from flooding.

Baseline Model Test Metrics:
- Accuracy Score: 0.668
- Recall Score: 0.201
- Precision Score: 0.201
- F1 Score: 0.201

Logistic Regression Test Metrics:


XGBoost Test Metrics:


## Visualizations
<img width="806" alt="skylar_chart" src="https://user-images.githubusercontent.com/79756630/145322462-9caeb33d-3c64-40b3-a2ca-88543aa38388.png">


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
