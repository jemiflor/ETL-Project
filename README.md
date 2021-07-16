# <p align="center">ETL-Project</p>

## <p align="center">Title: Vacation - Things To Do By Country Report</p>



### Introduction:
Often planning a vacation's first step involve getting a list of things to do and match the results with our interests to plan our getaway. The goal of this project was to create and curate a database with the top 20 things to do by country using the ETL process and help discover and experience the most incredible places and things to do on our next globe-trotting adventure. This project extracts data from the data sources given below, transforms the extracted dataset, and loads the data into a Postgresql database.

#### Data Source: 
1. List of countries:- https://www.geonames.org/countries/
2. Google place text search api:- https://maps.geoogleapis.com/maps/api/place/textsearch/json


### Extract: 
The GeoNames website had a webpage that listed all countries with geographical data. Pandas `read_html` was used to scrape the data from the Geonames countries web page and was converted to a data frame.
The data frame was then iterated and country name was used as a parameter for the google place test search api to get top 20 things to do (ex: <https://maps.googleapis.com/maps/api/place/textsearch/json?query=things+to+do,+andorra&language=en&key=your_api_key>). The results from the api were used to create a dictionary list of things to do.
> ##### *Limitation: An attempt to get the average temperature (min and max) and historical data for each place of interest from the OpenWeatherMap API using the latitiude and longitude information obtained from the google place search api but were limited by OpenWeatherMap daily quota limit and subscription costs*

### Transform:
The countries' data frame (created using pandas) and the dictionary list of things to do (created using google API) were then transformed to a single `country_attraction_df`  dataframe with `country_id` as an index.

### Load:
The `country_attraction_df` was then used to create a postgres database using SQlAclchemy.

### Next Steps:
Try to get the climate data from OpenWeatherMap API, 100 requests a day over some time for three months to augment the `ThingsToDoDb` Postgres database. Also, search for historical weather data and use it for statistical analysis for predicting weather to plan our next globe-trotting adventure!
