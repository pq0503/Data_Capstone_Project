*/

This is the SQL script used to import, compile and analyse the Cyclistic Case 
This code script is part of full capstone project
The scrip includeds 10 steps executing from combining, arranging to cleaning the data and prepare for later analysis

*/

---SQL SCRIPT------------------------------------------------------------------
step 1: Merging the data of 12 months into 1 “aggregate_table” using UNION function:

SELECT *  
FROM `beaming-surfer-359923.trip_data_2021.month_1` 
union all
SELECT *  
FROM `beaming-surfer-359923.trip_data_2021.month_2` 
union all
SELECT *  
FROM `beaming-surfer-359923.trip_data_2021.month_3`
union all
SELECT *  
FROM `beaming-surfer-359923.trip_data_2021.month_4`
union all
SELECT *  
FROM `beaming-surfer-359923.trip_data_2021.month_5`
union all
SELECT *  
FROM `beaming-surfer-359923.trip_data_2021.month_6`
union all
SELECT *  
FROM `beaming-surfer-359923.trip_data_2021.month_7`
union all
SELECT *  
FROM `beaming-surfer-359923.trip_data_2021.month_8`
union all
SELECT *  
FROM `beaming-surfer-359923.trip_data_2021.month_9`
union all
SELECT *  
FROM `beaming-surfer-359923.trip_data_2021.month_10`
union all
SELECT *  
FROM `beaming-surfer-359923.trip_data_2021.month_11`
union all
SELECT *  
FROM `beaming-surfer-359923.trip_data_2021.month_12`

---------------------------------------------------------

Step 2:Check whether all the trip_Id are unique or not and the result matched the total numbers of rows in a table:

SELECT  
count(distinct(ride_id))
FROM `beaming-surfer-359923.trip_data_2021.aggregate_2021`

----------------------------------------------------------

Step 3: Calculating the date, time difference (day and minute), create new table with these 2 new columns, arranging the table regarding the order of date, minute difference respectively:

SELECT
ride_id, rideable_type, started_at,ended_at,start_station_name,start_station_id,end_station_name,end_station_id,start_lat,start_lng,end_lat,end_lng,member_casual,  
date_diff(ended_at,started_at,day) as date_dif,
datetime_diff(ended_at,started_at,minute) as minute_dif
FROM `beaming-surfer-359923.trip_data_2021.aggregate_2021` 
order by date_dif, minute_dif

-----------------------------------------------------------

Step 4:Erasing all the columns with null value in any columns (the data is huge enough for us to erase since the null value may skew the result)

delete
FROM `beaming-surfer-359923.trip_data_2021.aggregate_before_cleaning_1`
where rideable_type is null OR
started_at is null OR
ended_at is null or
start_station_name is null or
start_station_id is null or
end_station_name is null or
end_station_id is null or
start_lat is null or
start_lng is null or
end_lat is null or
end_lng is null or
member_casual is null

---------------------------------------------------------------

Step 5: Erasing absurd data based on date, minute difference (can not be negative and can not be 0 in both 2 columns because it does not make sense)

delete 
FROM `beaming-surfer-359923.trip_data_2021.aggregate_before_cleaning_1`
where
(date_dif < 0 or minute_dif < 0) or (date_dif = 0 and minute_dif = 0)

-----------------------------------------------------------------

Step 6: Checking for duplicate values in all the columns → still have the same number of rows

SELECT  
distinct *
FROM `beaming-surfer-359923.trip_data_2021.aggregate_cleaned`

-------------------------------------------------------------------

Step 7: Checking the integrity of categorized columns

SELECT
distinct(member_casual) 
FROM `beaming-surfer-359923.trip_data_2021.aggregate_before_cleaning_1` 

SELECT
distinct(rideable_type) 
FROM `beaming-surfer-359923.trip_data_2021.aggregate_before_cleaning_1` 

---------------------------------------------------------------------

Step 8: Regarding the started day, turned it into day in a week for analyzing purposes.

SELECT 
ride_id,
started_at,
EXTRACT(DAYOFWEEK FROM started_at) as day_as_number,
CASE
when EXTRACT(DAYOFWEEK FROM started_at) = 1 then "Sunday"
when EXTRACT(DAYOFWEEK FROM started_at) = 2 then  "Monday"
when EXTRACT(DAYOFWEEK FROM started_at) = 3 then  "Tuesday"
when EXTRACT(DAYOFWEEK FROM started_at) = 4 then  "Wednesday"
when EXTRACT(DAYOFWEEK FROM started_at) = 5 then  "Thursday"
when EXTRACT(DAYOFWEEK FROM started_at) = 6 then  "Friday"
else  "Saturday"
end day_of_week
FROM `beaming-surfer-359923.trip_data_2021.aggregate_before_cleaning_1` 

