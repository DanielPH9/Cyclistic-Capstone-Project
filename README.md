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


<img src="https://github.com/DanielPH9/Cyclistic-Capstone-Project/blob/main/rides_per_user_type.png" width="500">

We can see that the number of annual members is larger than the number of casual users; however, the last ones use the bikes for longer time on average. There is also a very large ride made by a casual user. We will investigate that further.

Next, let's explore the type of bike preferred for each type of users:

```SQL
SELECT 
  rideable_type,
  member_casual,
  COUNT(ride_length) AS num_rides,
  MIN(ride_length) AS min_ride_duration,
  MAX(ride_length) AS max_ride_duration,
  ROUND(AVG(ride_length),2) AS average_ride_length
FROM city_bike_dataset_capstone.data_2023
WHERE ride_length > 0
GROUP BY rideable_type, member_casual
```

##### Output:

| rideable_type |	member_casual |	num_rides |	min_ride_duration |	max_ride_duration |	average_ride_length |
|---------------|---------------|-----------|-------------------|-------------------|---------------------|
|electric_bike|	member|	1774327|	1|	481|	11.05|
|electric_bike|	casual|	1063621	|1|	480|	14.29|
|classic_bike|	casual|	864555	|1|	1559|	32.02|
|classic_bike|	member|	1790185	|1|	1559|	13.66|
|docked_bike|	casual	|77574	|1|	98489|	184.0|

<img src="https://github.com/DanielPH9/Cyclistic-Capstone-Project/blob/main/rides_per_rideable_type_members.png" width="500"> 
<img src="https://github.com/DanielPH9/Cyclistic-Capstone-Project/blob/main/rides_per_rideable_type_casuals.png" width="500">

We can observe that the most popular type of bike among the casual users is the electric bike, followed by the classic one. In the case of the annual members they equally like both types of bikes. 
As a remark we notice that the docked bikes are only used by casual users, and in less than 4% of their rides. 
Another remark is that the longest ride of all the data was made by a casual user with a docked bike. 

To explore the behaviour of the different users per month, we use the following:

```SQL
SELECT 
  month,
  member_casual,
  COUNT(ride_length) AS num_rides,
  ROUND(AVG(ride_length),2) AS average_ride_length
FROM city_bike_dataset_capstone.data_2023
WHERE ride_length > 0
GROUP BY month, member_casual
ORDER BY num_rides DESC
```

##### Output:

|month|	member_casual|	num_rides|	average_ride_length|
|-----|--------------|-----------|---------------------|
|8|	member|	449587|	13.61|
|7|	member|	424922|	13.56|
|6	|member	|407789	|13.04|
|9|	member|	396288|	12.93|
|5|	member|	359580|	12.94|
|10|	member|	352461|	11.91|
|7|	casual|	322565|	32.71|
|8|	casual|	303735|	35.60|
|6|	casual|	293046|	29.73|
|4|	member|	269086	|11.63|
|11	|member	|258852|	11.31|
|9	|casual	|255766	|25.26|
|5	|casual	|227375|	28.87|
|3	|member|	189322	|10.33|
|10	|casual|	172959|	22.91|
|12|	member|	168723|	11.20|
|1|	member|	145276|	10.21|
|2|	member|	142626|	10.57|
|4|	casual|	142521|	28.09|
|11|	casual|	96262|	19.83|
|3|	casual|	60279|	21.59|
|12|	casual|	50587|	19.86|
|2|	casual|	41818|	23.36|
|1|	casual|	38837|	23.10|

<img src="https://github.com/DanielPH9/Cyclistic-Capstone-Project/blob/main/rides_per_month.png">

We can observe that the most popular months are when temperatures are more favorable for riding bikes. According to the visualization, the most popular months are from april to november, finding its peak in july-august. Also, we can observe that irrespective of the month, the annual members tend to ride their bikes for the same amount od time on average, but the casual users tend to use their bikes for longer time during august. 

Let's explore what happens inside a week:

```SQL
SELECT 
  day_of_week,
  member_casual,
  COUNT(ride_length) AS num_rides,
  MIN(ride_length) AS min_ride_duration,
  MAX(ride_length) AS max_ride_duration,
  ROUND(AVG(ride_length),2) AS average_ride_length
FROM city_bike_dataset_capstone.data_2023
WHERE ride_length > 0
GROUP BY day_of_week, member_casual
ORDER BY num_rides DESC
```

##### Output:

|day_of_week|	member_casual|	num_rides|	min_ride_duration|	max_ride_duration|	average_ride_length|
|----|----|----|----|----|----|
|5|	member|	573822|	1|	1499|	11.85|
|4|	member|	571585|	1	|1499	|11.76|
|3|	member|	561963|	1	|1499	|11.83|
|6|	member|	517281|	1	|1499	|12.32|
|2|	member|	481944|	1|	1499|	11.71|
|7|	member|	459879|	1|	1559|	13.83|
|7|	casual|	399905|	1|	64009|	32.5|
|1|	member|	398038|	1|	1500|	13.87|
|1|	casual|	326829|	1|	62867|	33.25|
|6|	casual|	303857|	1|	79775|	27.48|
|5|	casual|	263642|	1|	92569|	24.88|
|4|	casual|	242761|	1|	98489|	24.44|
|3|	casual|	239914|	1|	64171|	25.24|
|2|	casual|	228842|	1|	83382|	27.94|

<img src="https://github.com/DanielPH9/Cyclistic-Capstone-Project/blob/main/rides_per_weekday.png">

We can see that annual members use more the bikes during weekdays (Monday to Friday), while casual users use more the bikes during the weekends, and for longer periods of time.

Finally, let's visualize in a map what are the most popular pick-up points for casual users:

```SQL
SELECT 
  MAX(start_station_name) AS station_name,
  start_lat,
  start_lng,
  COUNT(ride_id) AS num_rides,
  COUNTIF(member_casual = "member") AS rides_by_members,
  COUNTIF(member_casual = "casual") AS rides_by_casuals
FROM city_bike_dataset_capstone.data_2023
GROUP BY start_lat, start_lng
ORDER BY num_rides DESC
LIMIT 2000
```

<img src="https://github.com/DanielPH9/Cyclistic-Capstone-Project/blob/main/rides_per_coordinates.png">

In the previous map we can visualize the started locations of the rides. Some features of the map are:
* Size of the Points: it is proportional to the number of rides initiated in those geographic coordinates. 
* Color: it indicates the percentage of rides initiated by casual users (blue indicates more than 50% of trips were initiated by casual users).
* Arrow: it indicates the most popular starting point for casual users, that corresponds to the station "Streeter Dr & Grand Ave".

In general, we can see that the stations that are closer to the coast are more popular among the casual users. Those locations away from the city are dominated by casual users as well, but from the size of the points we conclude that the number of users is quite small.

## Key Findings:
In this project, our task was to study how do annual members and casual riders use Cyclistic bikes differently.
After analyzing the provided data of 2023 of Cyclistic, we found that:
* Almost 64% of the rides were made by annual members.
* Casual users prefer electric bikes over classic and docked bikes, while annual members equally prefer electric and classic bikes.
* The docked bikes are not very popular, since they were only used by casual users, and in less than 4% of their rides.
* Both casual users and annual members prefer using the bikes between April and November.
* Casual users use the bikes for longer periods of time.
* Casual users use more the bikes during the weekends, while annual members use them more from Monday to Friday.
* "Streeter Dr & Grand Ave" is the station where more rides started, and over 70% were started by casual users.

## Recomendations:
My top three recomendations are:
* The marketing campaign should be made between the months of April and November, especially during july and august.
* The marketing campaign should be made closer to the coast for larger visibility of casual users. 
* Offer a discount for members using the bikes during the weekend, and for longer periods of time. This should be an incentive for the casual users to become annual members.
