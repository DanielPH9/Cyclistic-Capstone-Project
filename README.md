# Google Data Analytics Capstone Project: Cyclistic 🚴

## Case study: How does a bike-share navigate speedy success?

## Introduction:
Welcome to my analysis for the Cyclistic bike-share case study!
Cyclistic is a fictional company that in 2016, launched a successful bike-share offering. 
It has a large fleet of bicycles that are geotracked and locked into a network of several stations across Chicago. The bikes can be unlocked from one station and returned to any other station in the system anytime.

Cyclistic offers three different plans: 
* single-ride passes, 
* full-day passes, 
* annual memberships. 

Customers who purchase single-ride or full-day passes are referred to as casual riders. 
Customers who purchase annual memberships are Cyclistic members. 

Cyclistic’s finance analysts have concluded that annual members are much more profitable than casual riders and they seek to maximize the number of annual members to guarantee future growth. The goal is clear: Design marketing strategies aimed at converting casual riders into annual members. 
Three questions will guide the future marketing program:
1. How do annual members and casual riders use Cyclistic bikes differently?
2. Why would casual riders buy Cyclistic annual memberships?
3. How can Cyclistic use digital media to influence casual riders to become members?

### Business Task:
As a junior data analyst in Cyclistic, my task is to find and analyze how do annual members and casual riders use Cyclistic bikes differently and deliver my top three recommendations for the marketing strategies. 

### Data Sources:
The data used in this project is the DIVVY dataset, used under this [licence](http://divvybikes.com/data-license-agreement).

The dataset contained the data of Cyclistic trips on the year 2023 (from January to December) in twelve .CSV files (one for each month).
The data contained the following columns per type of data:
* STRING: ride_id, rideable_type, start_station_name, start_station_id, end_station_name, end_station_id, member_casual.
* TIMESTAMP: started_at, ended_at.
* FLOAT: start_lat, start_lng, end_lat, end_lng.

In total, there were over 5.5 millions of rides during 2023. Due to the extension of this data I decided to use BigQuery for the analysis and Tableau for visualizations.

### Data Cleaning and Manipulation Documentation:
First I created a data set in BigQuery named 'city_bike_dataset_capstone', then created one table for each month ('data_jan', 'data_feb', ..., 'data_dec'). 
After uploading all the data to BigQuery, it was convenient to unify all the data in a single table to simplify the analysis. Also, three new columns were created:
1. ride_length,
2. day_of_week,
3. month.

The first one is used to measure the duration of each ride based on the initialization (started_at) and ending (ended_at) times of each ride.
The last two new columns are directly obtained from the initialization time (started_at).
As a final modification, some columns were not considered in the analysis:
* start_station_id,
* end_station_name,
* end_station_id,
* started_at,
* ended_at,
* end_lat,
* end_lng.

The output of the following query was saved in a table named data_2023:

<details>
  <summary>Show Code</summary>
  
```SQL
SELECT 
  DISTINCT ride_id, 
  rideable_type,
  ride_length,
  day_of_week,
  month,
  member_casual,
  start_station_name,
  start_lat,
  start_lng
FROM
(
    SELECT 
      ride_id, 
      rideable_type,
      TIMESTAMP_DIFF(ended_at, started_at, minute) AS ride_length,
      EXTRACT (dayofweek FROM started_at) AS day_of_week,
      EXTRACT (month FROM started_at) AS month,
      member_casual,
      start_station_name,
      start_lat,
      start_lng
    FROM city_bike_dataset_capstone.data_jan jan
    UNION ALL
    SELECT 
      ride_id, 
      rideable_type,
      TIMESTAMP_DIFF(ended_at, started_at, minute) AS ride_length,
      EXTRACT (dayofweek FROM started_at) AS day_of_week,
      EXTRACT (month FROM started_at) AS month,
      member_casual,
      start_station_name,
      start_lat,
      start_lng
    FROM city_bike_dataset_capstone.data_feb feb
    UNION ALL
    SELECT 
      ride_id, 
      rideable_type,
      TIMESTAMP_DIFF(ended_at, started_at, minute) AS ride_length,
      EXTRACT (dayofweek FROM started_at) AS day_of_week,
      EXTRACT (month FROM started_at) AS month,
      member_casual,
      start_station_name,
      start_lat,
      start_lng
    FROM city_bike_dataset_capstone.data_mar mar
    UNION ALL
    SELECT 
      ride_id, 
      rideable_type,
      TIMESTAMP_DIFF(ended_at, started_at, minute) AS ride_length,
      EXTRACT (dayofweek FROM started_at) AS day_of_week,
      EXTRACT (month FROM started_at) AS month,
      member_casual,
      start_station_name,
      start_lat,
      start_lng
    FROM city_bike_dataset_capstone.data_apr apr
    UNION ALL
    SELECT 
      ride_id, 
      rideable_type,
      TIMESTAMP_DIFF(ended_at, started_at, minute) AS ride_length,
      EXTRACT (dayofweek FROM started_at) AS day_of_week,
      EXTRACT (month FROM started_at) AS month,
      member_casual,
      start_station_name,
      start_lat,
      start_lng
    FROM city_bike_dataset_capstone.data_may may
    UNION ALL
    SELECT 
      ride_id, 
      rideable_type,
      TIMESTAMP_DIFF(ended_at, started_at, minute) AS ride_length,
      EXTRACT (dayofweek FROM started_at) AS day_of_week,
      EXTRACT (month FROM started_at) AS month,
      member_casual,
      start_station_name,
      start_lat,
      start_lng
    FROM city_bike_dataset_capstone.data_jun jun
    UNION ALL
    SELECT 
      ride_id, 
      rideable_type,
      TIMESTAMP_DIFF(ended_at, started_at, minute) AS ride_length,
      EXTRACT (dayofweek FROM started_at) AS day_of_week,
      EXTRACT (month FROM started_at) AS month,
      member_casual,
      start_station_name,
      start_lat,
      start_lng
    FROM city_bike_dataset_capstone.data_jul jul
    UNION ALL
    SELECT 
      ride_id, 
      rideable_type,
      TIMESTAMP_DIFF(ended_at, started_at, minute) AS ride_length,
      EXTRACT (dayofweek FROM started_at) AS day_of_week,
      EXTRACT (month FROM started_at) AS month,
      member_casual,
      start_station_name,
      start_lat,
      start_lng
    FROM city_bike_dataset_capstone.data_aug aug
    UNION ALL
    SELECT 
      ride_id, 
      rideable_type,
      TIMESTAMP_DIFF(ended_at, started_at, minute) AS ride_length,
      EXTRACT (dayofweek FROM started_at) AS day_of_week,
      EXTRACT (month FROM started_at) AS month,
      member_casual,
      start_station_name,
      start_lat,
      start_lng
    FROM city_bike_dataset_capstone.data_sep sep
    UNION ALL
    SELECT 
      ride_id, 
      rideable_type,
      TIMESTAMP_DIFF(ended_at, started_at, minute) AS ride_length,
      EXTRACT (dayofweek FROM started_at) AS day_of_week,
      EXTRACT (month FROM started_at) AS month,
      member_casual,
      start_station_name,
      start_lat,
      start_lng
    FROM city_bike_dataset_capstone.data_oct oct
    UNION ALL
    SELECT 
      ride_id, 
      rideable_type,
      TIMESTAMP_DIFF(ended_at, started_at, minute) AS ride_length,
      EXTRACT (dayofweek FROM started_at) AS day_of_week,
      EXTRACT (month FROM started_at) AS month,
      member_casual,
      start_station_name,
      start_lat,
      start_lng
    FROM city_bike_dataset_capstone.data_nov nov
    UNION ALL
    SELECT 
      ride_id, 
      rideable_type,
      TIMESTAMP_DIFF(ended_at, started_at, minute) AS ride_length,
      EXTRACT (dayofweek FROM started_at) AS day_of_week,
      EXTRACT (month FROM started_at) AS month,
      member_casual,
      start_station_name,
      start_lat,
      start_lng
    FROM city_bike_dataset_capstone.data_dec dec
    ORDER BY ride_length DESC
) AS t1
WHERE t1.ride_length > 0

```
</details>

#### Observations: 
* All possible duplicate values were removed using 'DISTINCT ride_id' when querying the table containing the union of the data of all months.
* Some rides had initialization date later than the ending date, which is obviously wrong. This lead to negative values in the 'ride_length' column. All those entries were filtered out at the end of the query using 'WHERE t1.ride_length > 0', since we are only interested in the rides lasting at least one minute.
* Some initial station names are missing, but the latitude and longitude are not, which is enough for the geographic visualization. 
* At this point the data is ready for analysis.
​
## Analysis and Visualizations:
We can start our analysis by inspecting some statistics of the different types of users:

```SQL
SELECT 
  member_casual,
  COUNT(ride_length) AS total_rides,
  MIN(ride_length) AS shortest_ride,
  MAX(ride_length) AS longest_ride,
  AVG(ride_length) AS average_ride_duration
FROM city_bike_dataset_capstone.data_2023
GROUP BY member_casual
```

##### Output: 

| member_casual | total_rides | shortest_ride | longest_ride | average_ride_duration |
|---------------|-------------|---------------|--------------|-----------------------|
| member | 3660698 | 0 | 1559 | 12.037 |
| casual| 2059179 | 0 | 98489 | 27.76 |

[Visualization](rides_per_user_type.pdf)

We can see that the number of annual members is larger than the number of casual users; however, the last ones use the bikes for longer time on average. There is also a very large ride made by a casual user. We will investigate that further.

Next, let's explore the type of bike preferred for each type of users:

```SQL
SELECT 
  rideable_type,
  member_casual,
  COUNT(ride_length) AS num_rides,
  MIN(ride_length) AS min_ride_duration,
  MAX(ride_length) AS max_ride_duration,
  AVG(ride_length) AS average_ride_length
FROM city_bike_dataset_capstone.data_2023
WHERE ride_length > 0
GROUP BY rideable_type, member_casual
```

| rideable_type |	member_casual |	num_rides |	min_ride_duration |	max_ride_duration |	average_ride_length |
|---------------|---------------|-----------|-------------------|-------------------|---------------------|
|electric_bike|	member|	1774327|	1|	481|	11.05|
|electric_bike|	casual|	1063621	|1|	480|	14.29|
|classic_bike|	casual|	864555	|1|	1559|	32.02|
|classic_bike|	member|	1790185	|1|	1559|	13.66|
|docked_bike|	casual	|77574	|1|	98489|	184.0|

[Visualization for members](rides_per_rideable_type_members.pdf)
[Visualization for casuals](rides_per_rideable_type_casuals.pdf)

