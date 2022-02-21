# surfs_up
Data retrieval and display using SQLAlchemy, SQLite and Flask.

Statistical analysis on queried data using min, max, mean, standard deviation.

## Overview

This exercise runs analytics on weather data stored in SQLite in order to determine the viability of opening a year round surf and ice cream shop on the island of Oahu.

### Tools
- Python 3.7.11
- SQLite
- SQLAlchemy
- Jupyter Notebook

## Results
Using SQLalchemy, two queries are performed against the SQLite db containing weather information for the island of Oahu.  The first query pulls all temperatures for the month of June, the second for the month of December.  These data points are converted into dataFrames and statistical analysis is performed using the .describe() function.

| June  | December |
|---|---|
|![June Temps](/Resources/June_temps.png)  |                 ![December Temps](/Resources/December_temps.png)|

As you can see from the analysis
- Temperatures are nice in both December and June.  It is moderately cooler in December with an average temperature of 71 degrees Fahrenheit, while June tends to be on average four degrees warmer.
- There is slightly more variance in temperatures in December than June.  December has a standard deviation of 3.75; June temps have a 3.26 standard deviation.  The lower quartile in December may be cool for ice cream, although not for many people coming from less temperate climates.
- There are more temperature recordings in June (1700) than December (1517) despite December being a longer month. 

## Summary
The temperature analysis for Oahu shows that temperatures are highly favorable for a surf and ice cream shop in summer (June) and winter (December).  Additional queries could be performed for rainfall amounts in summer, fall, winter and spring to determine if high rain fall amounts will impact surfing opportunities.  

Rainfall analysis could be performed using the following queries and dataFrames:

```
# Query precipitation for june and december
juneresults = session.query(Measurement.prcp).filter(func.strftime("%m", Measurement.date) == "06").all()
decresults = session.query(Measurement.prcp).filter(func.strftime("%m", Measurement.date) == "12").all()

session.close()

# convert query results to lists
june_rain = list(np.ravel(juneresults))
dec_rain = list(np.ravel(decresults))

# Add to dataFrames
june_rain_df = pd.DataFrame(june_rain, columns=["June Precipitation"])
dec_rain_df = pd.DataFrame(dec_rain, columns=["December Precipitation"])

```

Further analysis could drill down deeper to the locations of the measurements in order to determine temperature and rainfall amounts at more granular locations throughout the island. 
