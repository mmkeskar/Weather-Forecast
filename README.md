# Weather-Forecast
This repository contains a project that aims to forecast temperature based on previously seen trends and data.

## Problem Statement
The purpose of this project is to predict the future temperature based on the historical data provided. 

## Methodology
In order to model the temperature and predict the temperature in celsius in teh future, I have implemented a two step methodology. First, some EDA needs to be performed on the available data. EDA is a very important part of any predicive task. It is important to look at the data that we have and figure out some basic statistics, correlations between variables, and pre-processing the data we have. Performing this data analysis gives a perspective in the kind of model we would have to build to be able to best model our target variables based on the available data.

The next step is to build a model to predict the target variable based on the selected features from the EDA.

## EDA
I looked at all the 

## XGBoost Model

## LSTM time series modeling
While predicting the future temperature, we are less likely to have access to all the feaures like the humidity, pressure, uv index, etc. We will most likely only have access to the latitude of teh region in question and the time when the forcecast has to be made. It would thus make more sense to build a model that only uses the latitude and the time to forecast the temperature. This will take us to time series modeling.

From the EDA, it was clear that there were visibile trends in the temperature depending on the time, but these trends were different for different bands of the latitude values. One idea I came up with was to break the data up into groups based on different bands of the latitude values and learn a time series model for each band group. But this is highly impractical since that would require me to train an unreasonable number of models. 

I was looking for a model that would be able to model temperuature as follows:
$$ Temperature = f_l(t) $$ where $$l$$ is the latitude and the $$t$$ is the time.

The LSTM model is great at time series modeling since it is able to model sequences with its memory element. LSTMs are also better at handling vanishing gradient problems. So I chose to use the LSTM model to model the trend in the temperature with an additional feature -- the latitude. I used 10 timesteps. The code is present in the file lstm-based-temperature-trend-prediction.ipynb. 
