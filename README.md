# Surf's Up Weather Analysis
## Overview
### Analysis Purpose
This project is an analysis of the Oahu's weather dataset to identify the weather trends, especially the temperature trends of June and December, in order to provide the weather information for the business plan of "Surf n' Shake shop" that will serve ice creams along with surfing boards on Oahu island, Hawaii. The analysis showing how weather can effect the business sustainability will be presented to W. Avy, the investor whose love lies in surfing.

### Resources
+ **Programming Languages:** Python3
+ **Software:** Jupyter Notebook
+ **Library:** Pandas, NumPy, SQLAlchemy
+ **Database:** [hawaii.sqlite](https://github.com/asama-w/surfs_up/blob/main/hawaii.sqlite)
+ **Analysis Code (Challenge code):** [SurfsUp_Challenge.ipynb](https://github.com/asama-w/surfs_up/blob/main/SurfsUp_Challenge.ipynb)


## Analysis Results
The temperature and precipitation data in this dataset was collected during year 2010 to 2017 from 9 different weather stations across Oahu Island, Hawaii. The following images show the outputs of the measurement table and station table overview retrieving from the sqlite dataset.

+ **Measurement table**:
The column names in the image are id, station, date, prcp, tobs, respectively.

<img src= https://github.com/asama-w/surfs_up/blob/main/Additional_Images/measurement_table_output.png width="50%" height="50%">

+ **Station table**:
The column names in the image are id, station, name, latitude, longitude, elevation, respectively.

<img src= https://github.com/asama-w/surfs_up/blob/main/Additional_Images/station_table_output.png width="55%" height="55%">

This analysis focuses on the temperature in June and December to have the year-round overview of the temperature trends.

### June Temperature VS December Temperature

<img src= https://github.com/asama-w/surfs_up/blob/main/Additional_Images/June_Temps.png width="21%" height="21%"><img src= https://github.com/asama-w/surfs_up/blob/main/Additional_Images/Dec_Temps.png width="25%" height="25%">

1. **Data count:** There are 1,700 temperature data for June and 1,517 data for December. 
  + June's temperature data in the database is collected from 2010 to 2017.
  + December's temperature data in the database is collected from 2010 to 2016 (no temperature data for the year 2017).

2. **Average temperature:** The difference in the average temperature between June and December is 3.4 °F
  + June's average temperature is 74.94 °F and December's average temperature is 71.04 °F

3. **Data Dispersion:** December's temperature data is slightly more spread out than June's data (lightly higher standard deviation)
  + The maximum temperatures of June and Dec are relatively similar (2 °F difference)
  + June: min temp = 64, max temp = 85, standard deviation = 3.26
  + December: min temp = 56, max = 83, standard deviation = 3.75


## Analysis Summary
### 1. Results Summary:
  + There is no extreme change in temperature when compared the months of June and December together. It can almost be equally hot in December as in June (maximum temperature is 83 and 85). There is a slightly higher difference in lowest temperatures of 8 F, December month feels cooler than June, but with no abrupt change in temperature.
  + This analysis only looked at how the temperature summary of June and December. However, the real temperature, or the feel-like temperature might differ depends on the weather conditions, such as warmer-feel on sunny days, cooler-feel on cloudy or rainy days.
  + Overall, it can be concluded from this temperature summary analysis that the year-round temperature, which is on the warmer side, is favorable for the Surf n' Shake shop, as there are warm days in December as well as in the mid-year month, and lowest temperature is not extreme, might not feel as cool if there is the sunshine.
  + This analysis only focuses on the summary statistics of temperature (mean, median, max, min). Additional analysis on the Oahu's weather may needed to see the trends over the years.
  + The following chart shows the temperature in the months of June and December.
 
<img src= https://github.com/asama-w/surfs_up/blob/main/Additional_Images/Temps_chart.png width="50%" height="50%">
  
### 2. Two additional queries to gather more data for June and December:

The additional queries are in the [SurfsUp_Challenge.ipynb](https://github.com/asama-w/surfs_up/blob/main/SurfsUp_Challenge.ipynb) following the challenge's code.

  1. **Precipitation Data:** Get the precipitation data for June and December to determine the year-round rainfalls.

example of the code:
```python
# June precipitation data
june_prcp = session.query(Measurement.date, Measurement.prcp).\
    filter(extract("month", Measurement.date) == "6").\
    order_by(Measurement.date).all()

# convert to DataFrame
june_prcp_df = pd.DataFrame(june_prcp, columns = ['Date', 'June Precipitation']).set_index('Date')
```
 <img src= https://github.com/asama-w/surfs_up/blob/main/Additional_Images/June_Precipitation.png width="20%" height="20%"><img src= https://github.com/asama-w/surfs_up/blob/main/Additional_Images/Dec_Precipitation.png width="20%" height="20%">
  
  2. **Average Precipitation per Station:** Determine the average precipitation per Station for June and December. As there 9 different stations, we can determine the more specific location for the shop that have the most suitable weather trends for the shop.

example of the code:
```python
# June precipitation data per station
june_prcp_by_station = session.query(Measurement.station, func.avg(Measurement.prcp)).\
    filter(extract("month", Measurement.date) == "6").\
    group_by(Measurement.station).\
    order_by(Measurement.station).all()
    
# Covert to DataFrame
june_prcp_by_station_df = pd.DataFrame(june_prcp_by_station, columns = ['Station', 'June Avg Precipitation']).set_index('Station')
june_prcp_by_station_df
```

<img src= https://github.com/asama-w/surfs_up/blob/main/Additional_Images/Avg_prcp_by%20_station_June.png width="20%" height="20%"><img src= https://github.com/asama-w/surfs_up/blob/main/Additional_Images/Avg_prcp_by%20_station_Dec.png width="20%" height="20%">

