# Sales-Forecasting

##### The Sales Forecasting Problem

Sales forecasting is all about using historical data to inform decision making.


On its core, this is a [time series](https://en.wikipedia.org/wiki/Time_series#:~:text=A%20time%20series%20is%20a,sequence%20of%20discrete%2Dtime%20data.) problem: given some data in time, we want to predict the dynamics of that same data in the future. To do this, we require some trainable model of these dynamics. 

##### Types of Forecasting Models

According to this [article](https://hbr.org/1971/07/how-to-choose-the-right-forecasting-technique) featured in the harvard business review, there are three types of Forecasting techniques:



- __Qualitative techniques__: usually involve expert opinion or information about special events.


- __Time series analysis and projection__: involve historical data,finding structure in the dynamics of the data like cyclical patterns, trends and growth rates.

##### Time Series Approach


Time series is a sequence of data points taken at successive, equally-spaced points in time that can be used to predict the future. 
A Time Series analysis model involves using historical data to forecast the future. It looks in the dataset for features such as trends, cyclical fluctuations, seasonality, and behavioral patterns.



The three key general ideas that are fundamental to consider, when dealing with a sales forecasting problem tackled from a time series perspective, are:


- Repeating patterns 
- Static patterns 
- Trends 

Now we'll look into each of these factors and write code that will allow us to understand them intuitively. After that, we will see what modern deep learning models could bring to the table. 

#### Repeating Patterns

When looking at a time series data, one element that we are looking for is a pattern that repeats in time. One key concept related to this idea is [__autocorrelation__](https://en.wikipedia.org/wiki/Autocorrelation#:~:text=Autocorrelation%2C%20also%20known%20as%20serial,the%20time%20lag%20between%20them.). 


Intuitively, ___autocorrelation corresponds to the similarity between observations as a function of the time lag between them.___

What does that mean? It refers to the idea of finding structure on the dynamics of the observations in a time-series by looking at the correlation between observations with themselves (i.e. "auto") at different time points. It is one of the main tools for finding repeating patterns.

The steps here will be:
- Load the dataset
- Get the total volume of sales for 45 stores
- Plot the total volume of sales between 2010 and 2013

##### Static patterns

As the expression suggests, the concept of a static pattern relates to the idea of something that does not change. 

In Time Series, the most famous proxy for this concept is [__stationarity__](https://en.wikipedia.org/wiki/Stationary_process), which refers to the statistical properties of a time series that remain static: the observations in a stationary time series are not dependent on time.



___Time series are stationary if they do not have trend or seasonal effects.___ 

The trend and seasonality will affect the value of the time series at different times. Traditionally, we would be looking for consistency over time, for example by using the mean or the variance of the observations. When a time series is stationary, it can be easier to model and statistical modeling methods usually assume or require the time series to be stationary to be effective. 



If you want to dig deeper into stationarity I recommend this [piece](https://towardsdatascience.com/stationarity-in-time-series-analysis-90c94f27322#:~:text=In%20the%20most%20intuitive%20sense,not%20itself%20change%20over%20time.) by @Shay Palachy.

#### Trends

A trend represents a tendency identified in our data. In a stock market scenario, this could be the trend of a given stock that appears to be going up or down. For Sales Forecasting, this is key: ___identifying a trend allows us to know the direction that our time-series is heading, which is fundamental for predicting the future of sales.___


We will use the [```fbprophet```](https://facebook.github.io/prophet/docs/quick_start.html) package to identify the overall trends for both our datasets. The steps will be:


- Select a range for the sales data
- Feed the data to the ```fbprophet.Prophet``` object as a dataframe with two columns: "ds" (for date) and "y" (data) 

- Run the model
- Plot the trend with an upper and lower bound


##### Traditional Time Series Models to Sales Forecasting




So far, we covered the basics of the sales forecasting problem and identified the main components of it from a time series perspective: repeating patterns, static patterns and the idea of a trend. If you want to dig deeper on time series, I recommend this [article](https://towardsdatascience.com/time-series-analysis-in-python-an-introduction-70d5a5b1d52a) by @Will Koehrsen.




Now we will look into the traditional time series approaches to deal with sales forecasting problems:




- Moving Average
- Exponential smoothing

- ARIMA

##### Moving Average
This model assumes that the next observation is the mean of all past observations and it can be used to identify interesting trends in the data. We can define a window to apply the moving average model to smooth the time series, and highlight different trends. 


Let's use the moving average model to predict the weather and sales. The steps will be:



- Select a range 
- Define a value for our moving average window
- Calculate the mean absolute error
- Plot an upper and lower bound for the rolling mean
- Plot the real data

##### Exponential Smoothing

Exponential smoothing is similar to moving average, but in this case a decreasing weight is assigned to each observation, so less importance is given to observations as we move further from the present. Such an assumption can be good and bad: it can be beneficial to decrease the weight of outdates information within the time-series dynamics, but it can be harmful when past information has some kind of permanent causal relationship with the dynamics of the data.  


##### Arima
ARIMA or Auto-regressive Integrated Moving Average is a time series model that aims to describe the auto-correlations in the time series data. It works well for short-term predictions and it can be useful to provide forecasted values for user-specified periods showing good results for demand, sales, planning, and production.

The parameters of the ARIMA model are defined as follows:

- p: The number of lag observations included in the model
- d: The number of times that the raw observations are differenced
- q: The size of the moving average window

