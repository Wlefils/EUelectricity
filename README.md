# Electricity Generation in the European Union
## Executive Summary

In this project, I evaluated renewable and non-renewable electricity generation in the European Union from 2017-2022. I used various techniques including moving averages, deseasonalization, linear regression, and simple exponential smoothing within Excel to analyze the time series data. The objective was to identify trends and seasonality to accurately forecast electricity generation from August 2022 to July 2023.

The first step was to plot the data. This showed apparent seasonality in renewable electricity generation, with notably more generation during winter, while non-renewables seemed consistently static year-round. To evaluate each model's accuracy, I computed error measures, including MSE, MAD, and most crucially, MAPE, which indicates the average deviation of the forecast from actual values, with lower values indicating more accurate forecasts.

![image](https://github.com/Wlefils/EUelectricity/assets/98787088/f841d296-7bc1-4276-89fb-fd4e412f35d2)

I found a three-month moving average to be the most accurate forecasting method for renewables, and its accuracy was further improved when combined with exponential smoothing and deseasonalization. In contrast, exponential smoothing, deseasonalization, and linear trend models exhibited higher error levels. The moving average method was able to smooth out both short-term fluctuations and longer-term trends in the data, hence its accuracy in this project. There is a positive trend in renewable energy generation when looking at all five years of data. Despite this, for the twelve months forecasted, my best model suggests renewables will see lower gigawatt-hours generated than in 2021-2022, more closely resembling their 2019-2022 numbers.

For non-renewables, the deseasonalized model stood out as the most precise forecasting method, contradicting my initial impression. Similar to renewable energy, the three-month moving average was highly accurate. There appears to be a slight negative trend in non-renewables when looking at all five years of data. The twelve month forecast anticipates a somewhat stable year ahead, with a minor uptick in gigawatt-hours in late spring and early summer 2023.

The final forecast chart and a comparative table of the error measures across models are presented below.

![image](https://github.com/Wlefils/EUelectricity/assets/98787088/d42a3e76-6e73-4bc3-b5ce-cc72032d6fb6)


![image](https://github.com/Wlefils/EUelectricity/assets/98787088/dceae680-1c0e-4c65-aaa4-876edde16705)


## Full Report 

### Project Objective
The objective of this project was to analyze electricity generation data from the European Union between 2017 and 2022, aiming to pinpoint trends and discern any seasonality present in either renewable and non-renewable energy production. My goal was to use statistical methods to develop a reliable model that could accurately forecast electricity generation from August 2022 to July 2023. With this model, I wanted to create high-quality predictions and insights based off this in-depth review of the existing data.

### Dataset Overview
This dataset contains monthly information regarding the monthly net electricity generation in the European Union from January 2017 to September 2022. The data is split by type of fuel (renewable and non-renewable) and measured in gigawatt-hours. This data was already cleaned; only minimal processing such as transposing values was conducted.  The raw data can be downloaded from Eurostat [here](https://ec.europa.eu/eurostat/databrowser/view/NRG_CB_PEM__custom_3671182/default/table).

### Analytical Tools and Techniques Used
#### Excel
Excel was my tool of choice for this project. It's excellent at performing ad-hoc analysis and provides a straightforward platform to manipulate data and visualize results efficiently and effectively. The relatively small size of the dataset meant that Excel's drawbacks in terms of handling large numbers of rows or complex data modeling meant that using a tool like R was less necessary for this specific project. I primarily utilized the Data Analysis ToolPak, specifically the linear regression portion. Excel's visualization tools are limited compared to BI tools like Tableau, but this project only needed simple line charts and tables, so it was more than serviceable.

#### Statistical Techniques
The following statistical techniques were used to determine and design the best model and the subsequent forecast:

- Moving Averages
- Deseasonalization
- Linear Regression
- Exponential Smoothing
- Model Evaluation: Error measures including MAPE, MSE, and MAD were used to evaluate the accuracy of the models.

## Detailed Analysis & Findings
### Initial Observations
- Apparent seasonality in Renewable energy electricity generation, especially during winter months.
- Non-renewable electricity generation appeared relatively static across months.

### Model Results and Insights
#### Three-Period Moving Average Model and Seasonal Adjustment
The first model deployed was the three-period moving average model. I chose this model initially for its ability to smooth out short-term fluctuations and highlight longer-term trends. I expected that electricity generation would include cyclical trends in addition to seasonal variation, so the moving average model seemed very applicable. Admittedly, a three-period moving average model could be too simplistic depending on the data involved, which is why I explored other models as well.

To enhance the moving average model and account for the observed seasonality in the data, I calculated a seasonal index in Excel. This involved computing an average for each period (i.e., each month) across all years to identify seasonal patterns. Then, I created a Seasonal Index for each three-month period to further improve accuracy. This was achieved by created a centered moving average

Using the three-month seasonal index, I deseasonalized the data to create an unadjusted forecast. To deseasonalize the data, I divided the actual electricity generated by the seasonal index. This process essentially strips the original data of its seasonal fluctuations so we can gain a clearer view of the underlying trend. This deseasonalized data was used to generate an initial forecast, which was then adjusted for any observable trend in the data to produce a seasonally-adjusted moving average forecast. This adjustment was crucial to ensure that the forecast not only followed the observed trend but also accurately reflected the inherent seasonality of the original data.

To further refine this seasonally-adjusted forecast, I applied exponential smoothing, which allowed the model to place greater weight on more recent observations. This helped ensure that the forecast was more responsive to any short-term fluctuations or shifts in the trend. I utilized Excel's Solver to optimize the seasonally adjusted forecast further by incorporating exponential smoothing. I initially set alpha (smoothing factor), at 0.20. I picked this as the starting point so the model would give a relatively higher weight to the most recent observations while not ignoring past values. However, Solver adjusted this alpha up to 1.00 and set Beta (the smoothing factor for the overall trend) to 0. This means that the optimal forecast, actually puts full weight on the most recent observation and does not account for any trend in the data. I initially assumed that a more balanced approach would be optimal, the most accurate forecasts ended up completely prioritizing the most recent data points and not accounting for a trend within the model.

The seasonally-adjusted moving average model was an effective choice because it combined the simplicity and trend-highlighting capabilities of the moving average model with a seasonal adjustment to account for cyclical patterns in the data. I was able to ultimately develop a more accurate and predictive forecast. As with all forecasting, this does come with the caveat that it assumes future seasonal patterns will mirror those we've observed in the past.

##### Moving Average Model Results
 - **Renewable**: The MA(3) had the lowest MAPE of 5.09%. A combination of moving average, deseasonalization, and exponential smoothing reduced the MAPE to 4.39%.
 - **Non-Renewable**: MAPE for the non-renewable 3-Month moving average forecast was 2.81%. This was the second most accurate forecasting method for non-renewable electricity generation.

#### Linear Regression Models
The next model I designed was a linear regression model. This type of model is very useful for examining how a dependent variable (in this case, electricity generation) is influenced by one or more independent variables (e.g., the month in which the electricity is generated). In time-series data like this, certain periods tend to showcase seasonality, as previously established. Therefore I created dummy variables for each month to capture these patterns within the model. A dummy variable is simply a numerical variable to represent subgroups in the data. They are very helpful in that dummy variables allow us to quantify otherwise qualitative categories, by designating them as either a "0" or "1" value. For example, the December dummy variable column in Excel had a "0" input in every row except during the month of December, where it was denoted with a "1".

I created a total of four linear regression models for this project (two for each type of energy). The first model used dummy variables for each month, while the second model also included a trend variable.

##### Monthly Linear Regression without Trend Variable Results
- **Renewables:**
The model revealed that the month is a statistically significant factor in the variation in renewable electricity generation, explaining 57% of the variation in the data, as indicated by an adjusted R-Square of 0.57. Comparing each month against January (serving as a baseline), the coefficients suggested that January is typically colder than every other month. The p-values for December, March, and November were not statistically significant at the 0.05 confidence level, and February's p-value was not significant at the 0.01 level. This implies that the winter months, including March, do not significantly differ in terms of renewable electricity generation. The Significance F value was 0.00, indicating a solid model. This model on average, deviates from actual observations by 468.32 gigawatt hours, or 6.21%, marking it as the second-most accurate method for predicting renewable electricity generation.

-  **Non-renewables:**
Contrastingly, the linear regression model for non-renewable electricity generation presented a different story. An adjusted R-Square of 0.05 demonstrated only a very weak correlation between months and non-renewable electricity generation. The model, with a Significance F of 23%, suggested a non-negligible risk (23% chance) of the model being unreliable or "junk." A closer look at the p-values, when compared against January, revealed that most months were not statistically significantly different, indicating that non-renewable electricity generation remains relatively stable throughout the year with minor fluctuations. Despite all coefficients being negative, implying that January typically experiences the peak in non-renewable electricity generation, the differences were not statistically significant in most cases. The model, although providing a glimpse into the non-renewable electricity generation patterns, was the least accurate forecasting method for non-renewable electricity generation, being off by 130.12 gigawatt hours or 4.85% per observation on average.

##### Monthly Linear Regression with Trend Variable Results
In these models, I added a trend variable to try to account for any potential long-term trends in the data. By adding this trend variable, which in this case was a simple count of time periods, the model was fable to factor in any consistent increases or decreases in electricity generation over time. In theory this provides a more accurate, more nuanced model. However, in practice, this isn't always the case, as I discovered. The results of these models were far less accurate, less statistically significant, and ultimately less useful than the other models.

- **Renewables:**
In the case of renewable energy, introducing a trend variable to the linear regression model brought forth several key insights. The model’s MAPE and MAD were 8.03% and 609.84 were higher than the previous models, telling me that our model was getting worse, not better. The Adjusted R-Square value of 0.22 tells us that 22% of the variation in the renewable electricity generation can be explained by the month and the overall trend across the five years of data. The Significance F value of 0.01 tells us that the model might not be valid. This model was notably less accurate when compared to the model without the trend variable.

- **Non-Renewable:**
This model resulted in a MAPE of 4.04% and a MAD of 106.48. However, the p-values for the variables were not significant at the 0.05 confidence level, with the sole exception of February at the 0.04 level. The Adjusted R-Squared value here was 0.16, revealing that the model, inclusive of the month and overall trend, explained 16% of the variation in the data. The Significance F value was 0.04, indicating a 4% chance that the model is essentially junk. 


#### Monthly Deseasonalization Models
For the next model, I decided to deseasonalize the data by month, rather than by a three-period moving average. I did this to further explore what the linear regression models were indicating, that some months appeared to have statistically significant deviation in electricity generation from the average. 

![image](https://github.com/Wlefils/EUelectricity/assets/98787088/159b0417-ceb4-4a2c-baf6-db40d69fb49f)

I created a monthly seasonality index to quantify the seasonal influence for each month. I created Pivot Tables in Excel to aggregate the data properly. For each month, I averaged the electricity generation across all years in the dataset. Similarly, I computed the overall average electricity generated across all months and years in the data. I was able to dervice the seasonality index for each month by dividing the average generation for that month by the overall average; this tells us the proportional deviation of electricity generation in each month from the overall average.

I then used this index to deseasonalize the original electricity generation data. I used Excel’s VLOOKUP function to match the respective seasonality index to each observation based on its month. Each original observation was then divided by its corresponding seasonality index. This is very similar to the process in the moving average model, but the seasonality index was calculated for each month, rather than for each three-month period. As with the other models, once I had a deseasonlized forecast, I calculated the error measures to assess accuracy and reliability.

##### Monthly Deseasonalization Model Results

- **Renewables:**
The MAPE of the monthly deseasonalized forecast for non-renewables indicates that on average, our deseasonalized forecast is 8.83% away from the actual observed value of renewable electricity generation, in either direction. This is second the largest error of all methods attempted.

- **Non-Renewables:**
The MAPE of the monthly deseasonalized forecast of non-renewable electricity generation is 2.75%, meaning for each monthly observation it is off by about 75.06 gigawatt hours in either direction. This was the lowest MAPE, i.e. the most accurate forecasting method, for the non-renewable electricity generation. This should indicate that there actually is seasonality in the dataset.  When combined with the relative accuracy of the three-period moving average, it seems non-renewables seasonality is more closely tied to actual seasons than to months. This may due to less variation in each individual month.

![image](https://github.com/Wlefils/EUelectricity/assets/98787088/5441320b-1ca2-4dd4-93d4-c8ccbf2b06b4)


#### Exponential Smoothing Models
As I briefly mentioned in the moving average section, exponential smoothing uses a weighted average of past observations as the basis for future predictions. Essentially, it gives the heaviest weight to the most recent observation, with the weight assigned to past observations decaying exponentially as they recede into the past.  I opted to utilize exponential smoothing by itself to evaluate its effectiveness in the realm of electricity generation, which I expected to be subject to seasonal and cyclical variation. To implement this within Excel involved utilizing the exponential smoothing formula, which necessitates a smoothing parameter (α), to control the decay of weights for past observations.

##### Exponential Smoothing Model Results
 - **Renewables**: The renewable forecast with exponential smoothing has a MAPE of 9.72%, indicating that it is, on average, off by 727.88 gigawatt hours (the MAD) for each monthly observation. This is the worst MAPE for the renewable electricity generation forecasts. Note that the MAPE is lower, 5.97%, when averaging the observations per year rather than per month. Even with this lower value, it remains the least accurate forecast method for renewable electricity generation.

- **Non-Renewables**: The non-renewable forecast with exponential smoothing has a MAPE of 4.41%, indicating that it is, on average, off by 117.88 gigawatt hours for each monthly observation. This is the second worst MAPE for the non-renewable electricity generation forecasts. When averaging the years rather than months, the MAPE is even worse, at 5.76%.

![image](https://github.com/Wlefils/EUelectricity/assets/98787088/61c9c46a-3a73-42d3-86e0-75c28de3ccd3)

## Conclusion
![image](https://github.com/Wlefils/EUelectricity/assets/98787088/d8d30019-9c28-4a1a-854e-60729836cf52)

After analyzing the data, I found the most accurate forecasting method for both renewables and non-renewable electricity generation. For the former, I used a combination of moving average, deseasonalization, and exponential smoothing techniques, resulting in the lowest MAPE of 4.39%. The three-month moving average was the single most accurate technique (5.09%). For the latter, I found deseasonalization to be the most accurate (lowest MAPE of 2.75%), followed by moving average. Based on the fact that the deseasonalized forecast was the most accurate, I conclude that seasonality is present in the non-renewable electricty generation, despite it not being apparent when I first plotted it. More non-renewable electricity is generated during the winter months, and less in the summer months. The same is true in the case of renewable energy, although the seasonality is more pronounced in renewables. Additionally, there does appear to be a positive trend in renewable and a slight decline in non-renewable electricity generation over the five year duration of the dataset. 

For the 2022-23 Forecast, my best model predicts renewable generation will see a decline from its highs in 2021-2022, more closely resembling its 2019-2020 numbers. For non-renewables, my model predicts a pretty similar year to the previous one, with a bit of an uptick from 2022 to 2023 in the late spring-early summer months

