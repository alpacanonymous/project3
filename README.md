![kangaroos](https://github.com/aykim1127/project3/blob/main/images/kangaroos.jpeg)

# Predicting Rain Tomorrow in Australia
Authors: Angela Kim, Colin Pelzer, Daniel Burdeno, Steven Addison


## Overview
This project analyzes climate data of various locations in Australia and designs the best classification model to predict whether it will rain tomorrow based on different weather features such as relative humidity, cloud cover, and atmospheric pressure.

![map](https://github.com/aykim1127/project3/blob/main/images/map.png?raw=true)


## Business Problem
Agriculture is an essential part of Australia's economy, and rainfall plays a big role in its success. Real-time weather forecasting can help farmers make better decisions on how to tend to their crops. It's important to know what kinds of weather conditions (ie. relative humidity, hours of sunshine) will determine precipitation in order to implement the best methods to protect crops and secure a high and robust yield. For areas with low rainfall, it would be important to know if it will rain so that farmers know if they should prepare to irrigate their crops or not. For areas with high rainfall, farmers can use a predictive model to protect their crops from flooding. Another area of farming that depends on real-time rain forecasting is fertilizer application and timing. You want the appropriate amount of moisture in the soil so that the fertilizer can be worked in. Soil moisture also determines field workablity. Farmers can become more efficient in their operations and save costs on unnecessary irrigations and poor fertilization scheduling. <a href="#Sources">(source)</a>


## Data Understanding
The data comes from the [Australian Government Bureau of Meteorology](http://www.bom.gov.au/climate/data/) and covers climate statistics from 2007-2017, which was then compiled into a dataset found on [Kaggle](https://www.kaggle.com/jsphyg/weather-dataset-rattle-package). We supplemented this dataset with data from other sources <a href="#Sources">(see below)</a>. This dataset covers 49 locations from all over Australia and contains records for 22 weather features with their corresponding dates. Refer [here](https://rdrr.io/cran/rattle.data/man/weatherAUS.html) for description about each feature. After exploring and preparing the data, we designed a classification model to predict whether it will "Rain Tomorrow" in the various locations in Australia.


## Data Preparation & Analysis
The `weatherAUS` dataset contains 145,460 entries(rows) with 343,248 null values. The target for our models is `RainTomorrow`. Nearly every feature(column) has null values with the exception of `Date` and `Location`. We were able to fill in the majority of missing values in `Sunshine` using data provided by [BOM](http://www.bom.gov.au) and [Climate-Data.org](https://en.climate-data.org/oceania/australia-140/). We did this by creating a nested dictionary of each location with the mean values of `Sunshine` for each month. We extracted `Month` from `Date` then used a for loop to replace a null value for `Sunshine` based on `Location` and `Month`. All other missing values were imputed using sklearn's KNNImputer. We dropped `Evaporation` because about 43% of its values were missing, and we couldn't find any information to fill them in. We removed the three records of 9 within the `Cloud9am` and `Cloud3pm` columns under the assumption that they were misrecorded because the values range from 0-8 [oktas](https://en.wikipedia.org/wiki/Okta). All categorical features were encoded using sklearn's OneHotEncoder.

Click [here](https://github.com/aykim1127/project3/blob/main/data_prep_notebook.ipynb) for more details on our data preparation and analysis.

## Modeling
We chose <i>accuracy</i> as our primary evaluation metric for our models because predicting rain accurately is the most valuable information for farmers. If they are expecting no rain in a drier region, they can prepare sprinklers. If they are expecting rain in a wetter region, they can protect their crops from flooding. For our secondary objective, we wanted to increase <i>precision</i> while maximizing accuracy in order to maintain positive predictions.

#### Baseline Model
- Accuracy Score: 0.668
- Precision Score: 0.206

#### Logistic Regression
- Accuracy Score: 0.787
- Precision Score: 0.491

#### Decision Tree
- Accuracy Score: 0.842
- Precision Score: 0.686

#### Random Forest
- Accuracy Score: 0.843
- Precision Score: 0.786

#### Gradient Boost
- Accuracy Score: 0.856
- Precision Score: 0.724

#### XGBoost
- Accuracy Score: 0.862
- Precision Score: 0.740

#### XGBoost2
- Accuracy Score: 0.862
- Precision Score: 0.747

Click [here](https://github.com/aykim1127/project3/blob/main/modeling_notebook.ipynb) for further details on our iterative model approach.


## Visualizations
![accuracy chart](https://github.com/aykim1127/project3/blob/main/images/accuracy_chart.png)
![]()

## Conclusions
In conclusion, our best performing model was our second XGBoost model with an accuracy of 86.2 and precision of 74.7%. We also chose XGBoost for its fast computational power compared to the other models. This has potential to be used in the field where strong computers are scarce.

In addition to location, the features with the strongest effect on our model are afternoon weather conditions, specifically relative humidity, cloud cover, and max wind gust speed. Farmers can use this information to their advantage. By being conscious of humidity, amount of cloud cover, and wind gust speed, they can use our model to determine whether or not it will rain the next day or at least keep these features in mind to make educational guesses.

To view our presentation, click [here](https://www.canva.com/design/DAEx3uG5NIU/PnQ6UHDDkNjACTbod4degQ/view#4).


## Next Steps
With an accuracy of 86.2% and precision of 74.7%, we think we can do better. First, we would have to gather more data. Because our dataset was missing so many values, our top priority would be to extract the correct numbers from the Bureau of Meteorology or other resources. However, this would require more time and money.

We would also implement feature engineering, looking at things such as the change of some of these values and not just the exact recorded measurements.

Another important consideration is a multiple model approach. Because this model takes information from all over Australia, a country with an area of 2.97 million square miles, with multiple climates and subclimates, we believe designing multiple models for each distinguished climate would produce better results.

We must consider climate change. As global temperatures continue to increase, we must adjust our models to take erratic weather conditions into account.

Ultimately, we would like to predict further out than the day ahead.


## <a id="Sources">Sources</a>
- [Dataset on Kaggle](https://www.kaggle.com/jsphyg/weather-dataset-rattle-package)
- [Australian Government Bureau of Meteorology](http://www.bom.gov.au/climate/data/)
- [Description & Format of weatherAUS dataset](https://rdrr.io/cran/rattle.data/man/weatherAUS.html)
- [Climate-Data.org](https://en.climate-data.org/oceania/australia-140/)
- [The Role of Weather and Weather Forecasting in Agriculture](https://www.dtn.com/the-role-of-weather-and-weather-forecasting-in-agriculture/)
- [Weather Forecasting for the Farmer](https://www.agritechtomorrow.com/article/2020/02/weather-forecasting-for-the-farmer/11981)
- [Importance of Weather Forecasting in Modern Agriculture and Farming](https://tractorguru.in/tractor-blog/importance-of-weather-forecasting-in-modern-agriculture-and-farming)
- [Oktas](https://en.wikipedia.org/wiki/Okta)


## Repository Structure
```
├── [data]
│    ├── sunshine.py
│    ├── weatherAUS.csv
│    ├── X_test_KNNI.parquet
│    ├── X_train_KNNI.parquet
│    ├── y_test.parquet
│    └── y_train.parquet
├── [images]
├── .gitignore
├── README.md
├── presentation.pdf
├── data_prep_notebook.ipynb
└── modeling_notebook.ipynb
```
