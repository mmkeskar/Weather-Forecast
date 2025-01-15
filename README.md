# Weather-Forecast
This repository contains a project that aims to forecast temperature based on previously seen trends and data.

## Problem Statement
The purpose of this project is to predict the future temperature based on the historical data provided. 

## Methodology
In order to model the temperature and predict the temperature in celsius in the future, I have implemented a two step methodology. First, some EDA needs to be performed on the available data. EDA is a very important part of any predicive task. It is important to look at the data that we have and figure out some basic statistics, correlations between variables, and pre-processing the data we have. Performing this data analysis gives a perspective in the kind of model we would have to build to be able to best model our target variables based on the available data.

The next step is to build a model to predict the target variable based on the selected features from the EDA.

## EDA
The purpose behind the EDA was to perform feature selection and analyze the correlation among the variables present in the data. The eda-weather-data.ipynb notebook has a detailed EDA. From this EDA, we can see that the features humidity, pressure and uv index have a correlation with the temperature values. It is interesting to note that the trends in temperature with respect to time are seen for different countries. These countries can be classified or characterized by the latitudes and longitudes they are present at. I have tried to analyze this relationship by looking at the temperature values against the longitude and latitude values. We see a clear trend in the temperatures across time, but this trend exists only for bands of latitude values. There isn't much correlation between the longitude and temperature values and this makes sense. The sun's rays hit the earth's surface at different angles depending on the latitude values. However, the longitude values dont make a difference in the sun's rays. Thus, our data analysis aligns with our geographical knowledge as well. 

## XGBoost Model
In order to build an ensemble model that can use the features get from our EDA. An ensemble of decision trees (random forest) would be a great idea. We can use all our different features and predict the temperature in any region in the event that we know the humidity, pressure, UV index, and the time at which we want to predict the temperature for. I am using a better model than the random forest though -- the XGBoost model. The XGBoost model is better because it reduces overfitting. I have also tried to tune the model and tried out different hyperparameters. I have also plotted the predictions against the true values. This plot looks like a straight line, but the splot of of the line is less than 1. The slope should have been 1. This means that there is definitely scope for improvement. 

Even though I have implemented an XGBoost model here that uses all the features to predict the temperature, it is not exactly the correct approach. If we are tasked with predicting the temperature in teh future, we will likely not have access to the values such as humidity, pressure, and UV index. We will however know when we want to predict the temperature for and where we want to predict it for. Thus I have implemented another model that takes this into account and models the trend in temperature based on the location/region.

## LSTM time series modeling
While predicting the future temperature, we are less likely to have access to all the feaures like the humidity, pressure, uv index, etc. We will most likely only have access to the latitude of teh region in question and the time when the forcecast has to be made. It would thus make more sense to build a model that only uses the latitude and the time to forecast the temperature. This will take us to time series modeling.

From the EDA, it was clear that there were visibile trends in the temperature depending on the time, but these trends were different for different bands of the latitude values. One idea I came up with was to break the data up into groups based on different bands of the latitude values and learn a time series model for each band group. But this is highly impractical since that would require me to train an unreasonable number of models. 

I was looking for a model that would be able to model temperuature as follows:
$$ Temperature = f_l(t) $$ where $$l$$ is the latitude and the $$t$$ is the time.

The LSTM model is great at time series modeling since it is able to model sequences with its memory element. LSTMs are also better at handling vanishing gradient problems. So I chose to use the LSTM model to model the trend in the temperature with an additional feature -- the latitude. I used 10 timesteps. The code is present in the file lstm-based-temperature-trend-prediction.ipynb. 
