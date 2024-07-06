# Data Portfolio

This is my portfolio website!

:) 


# Data Portfolio:  Analyzing the Impact of Airline Loyalty Campaign Programs on Flight Bookings

# Table of contents 
- [Executive Summary](#executive-summary)
	-[Objectives](#objectives)
	-[User Story](#user-story)
	-[Problem Statement](#problem-statement)
- [Data Source](#data-source)
- [Methodology](#methodology)
	- [Stages](#stages)
	- [Tools](#tools)
- [Development](#development)  
- [Pseudocode](#pseudocode)
 	 - [Data Exploration](#data-exploration)
  	- [Data Cleaning](#data-cleaning)
  - [Transform the Data](#transform-the-data)- [Testing](#testing)
 	 - [Data Quality Tests](#data-quality-tests)
- [Analysis](#analysis)
  - [Exploratory Data Analysis](#exploratory-data-analysis)
 	 - [Findings](#findings)  
- [Visualization](#visualization)
  	- [Results](#results)
 	 - [DAX Measures](#dax-measures)

- [Recommendations](#recommendations)
 	 - [Potential ROI](#potential-roi)
  - [Potential Courses of Actions](#potential-courses-of-actions)
- [Feasibility](#feasibility)
- [Conclusion](#conclusion)


# Executive Summary

This project investigates the influence of airline loyalty campaigns on flight bookings and customer retention. By employing data analytics techniques, we aim to understand how these campaigns affect customer behavior and flight sales. The analysis will provide actionable insights to optimize campaign strategies, enhance customer loyalty, and boost airline revenues.

## Objectives
1.	Identify Patterns and Trends: Uncover patterns in customer booking behaviour influenced by various loyalty campaigns, such as promotions, rewards, and membership tiers.
2.	 Evaluate Customer Retention: Measure changes in customer retention rates attributable to loyalty campaigns by analysing repeat booking data and customer lifecycle metrics.
3.	Segment Analysis: Segment the customer base to identify which groups respond most positively to loyalty campaigns, based on demographic and booking behaviour characteristics.
4.	Analysis visualisation : Create a dashboard to visualise the results of the above objectives.
5.	Provide Recommendations: Offer data-driven recommendations to enhance the design and execution of future loyalty campaigns for improved effectiveness and customer satisfaction.


## User Story
As a Marketing Manager at Adventure Works Airlines,  my goal is to achieve a higher ROI on loyalty campaigns and ensure they are effectively driving flight bookings and customer retention. I need clear, actionable insights from data analysis to fine-tune our strategies. These insights will also be shown to the Executives as they require insights into the return on investment (ROI) of loyalty campaigns to make informed decisions about resource allocation.																					
## Problem Statement
Adventure Works Airlines invest significantly in loyalty campaigns without fully understanding their effectiveness. There is limited insight into how these campaigns influence booking patterns and customer retention. The lack of detailed analysis hinders the ability to optimize campaign strategies and maximize ROI. This project seeks to fill this gap by providing a comprehensive analysis of the impact of loyalty campaigns on flight bookings and customer behaviour.


# Data Source
- What data is needed to achieve our objective?
We need data on the Impact of Adventure Works Airlines’ Loyalty Campaign Programs on Flight Bookings that includes customer’s:
-	Customer Lifetime Value,
-	Enrolment Type,
-	Cancellation Year,
-	Cancellation Month
-	Total Flights Booked,
-	Distance,
-	Points Accumulated,
-	Points Redeemed,
-	Dollar Cost  Points  Redeemed 

 Where is the data coming from? 
The data is sourced from Kaggle (an Excel extract), [see here to find it.](w.kaggle.com/datasets/bhavyadhingra00020/top-100-social-media-influencers-2024-countrywise?resource=download). The tpes of data involved are structured and quantitative.

# Methodology
Regression Analysis was used to see the correlation between flights booked and points accumulated.

## Stages
- Developement
- Testing
- Analysis

## Tools 
| Tool | Purpose |
| --- | --- |
| Excel | Exploring the data |
| SQL Server | Cleaning, testing, and analyzing the data |
| Power BI | Visualizing the data via interactive dashboards |
| GitHub | Hosting the project documentation and version control |

# Development

## Pseudocode

- What's the general approach in creating this solution from start to finish?

1. Get the data
2. Explore the data in Excel
3. Load the data into SQL Server
4. Clean the data with SQL
5. Test the data with SQL
6. Visualize the data in Power BI
7. Generate the findings based on the insights
8. Write the documentation + commentary
9. Publish the data to GitHub Pages

## Data exploration: Observations
1.	There are two separate tables with containing important information. This means both tables must be merged to meet our objective
2.	The Column ‘Country’ only contains ‘Canada’
3.	There are at least 6 columns that contain the data we need for this analysis, indicating we have the necessary information needed without needing to contact the client for any more data
4.	Column Salary has 25% missing values,  Columns Cancellation Year and Cancellation Month has 87% missing values.
5.	Within the customer flight activity dataset  0.4% of rows are duplicates.
6.	The months in both datasets are integers and not characters
7.	We have more data than we need, so some of these columns would need to be removed

## Data Cleaning
The cleaned data should meet the following criteria and constraints:
•	Only relevant columns should be retained.
•	All data types should be appropriate for the contents of each column.
•	No column should contain null values, indicating complete data for all records.
•	No rows should contain duplicate values
### Steps to clean and shape the data into the desired format
1.	Remove unnecessary columns by only selecting the ones you need e.g postal_code and Country 
2.	Remove duplicate data within the customer flight activity dataset
3.	Replace missing values with 0 where Salary, cancellation_year and cancellation_month are null
4.	Replace the month number with the name of the month
5.	Replace 0 with ‘Active’ in cancellation_year and cancellation_month to show customer has not cancelled
6.	Change data type of months, cancellation_month and enrolment_month from integers to characters
7.	Make loyalty_number in customer flight activity a foreign key
### Dataset information
Below is a table outlining the constraints on our cleaned customer flight activity dataset:
| Property | Description |
| --- | --- |
| Number of Rows | 403, 760 |
| Number of Columns | 10 |

Below is a table outlining the constraints on our cleaned customer loyalty history dataset:
| Property | Description |
| --- | --- |
| Number of Rows | 16, 737 |
| Number of Columns | 15 |

### Tabular representation of the expected schema for the customer loyalty history data:
| Column Name | Data Type | Nullable | Key |
| --- | --- | --- | --- |
| loyalty_number | INTEGER | NO | PRIMARY KEY
| Country | VARCHAR | NO |
| Province | VARCHAR | NO |
| City | VARCHAR | NO |
| Country | VARCHAR | NO |
| Province | VARCHAR | NO |
| postal_code | VARCHAR | NO |
| Gender | VARCHAR | NO |
| Education | VARCHAR | NO |
| Salary | INTEGER | NO |
| marital_status | VARCHAR | NO |
| loyalty_card | VARCHAR | NO |
| clv | DECIMAL | NO |
| enrollment_type | VARCHAR | NO |
| enrollment_year | VARCHAR | NO |
| enrollment_month | VARCHAR | NO |
| cancellation_year | VARCHAR | NO |
cancellation_month | VARCHAR | NO |

### Tabular representation of the expected schema for the customer flight activity data:

| Column Name | Data Type | Nullable | Key |
| --- | --- | --- | --- |
| loyalty_number | INTEGER | NO | FOREIGN KEY
| Year | DATE | NO |
| Months | DATE | NO |
| flights_booked | INTEGER | NO |
| flights_with_companions | INTEGER | NO |
| total_flights | INTEGER | NO |
| distance | INTEGER | NO |
| points_accumulated | INTEGER | NO |
| points_redeemed | INTEGER | NO |
| dollar_cost_points_redeemed | INTEGER | NO |

### Transform the data
```sql
/*
# 1. Delete postal_code column by dropping it 
# 2. Select and  delete any duplicates within the dataset
# 3. Replace all null values with ‘0’  within the Salary column
# 4. Change data types for columns enrollment_month, cancellation_month and months to VARCHAR`
#5. Convert month number for columns enrollment_month, cancellation_month and months
 to name of the month
#6. Change data type for cancellation_year to VARCHAR
#7. Replace null values within cancellation_year and cancellation_month  with ‘Active’
#8. Make loyalty_number from customer_flight_activity a foreign key

-- 1.
ALTER TABLE customer_loyalty_history
DROP COLUMN postal_code;
-- 2.
WITH CTE AS (
    SELECT *,
           ROW_NUMBER() OVER (PARTITION BY loyalty_number, year, months, flights_booked, flights_with_companions, total_flights, distance, points_accumulated, points_redeemed, dollar_cost_points_redeemed ORDER BY loyalty_number) AS rn
    FROM customer_flight_activity
)
DELETE FROM CTE
WHERE rn > 1;
-- 3.
SELECT * FROM customer_loyalty_history WHERE 
Salary IS NULL
OR cancellation_year IS NULL
OR cancellation_month IS NULL;
 
UPDATE customer_loyalty_history
SET Salary = '0'
WHERE Salary IS NULL;
-- 4.
ALTER TABLE customer_loyalty_history
ALTER COLUMN enrollment_month varchar(20);

ALTER TABLE customer_loyalty_history
ALTER COLUMN cancellation_month varchar(20);

ALTER TABLE customer_flight_activity
ALTER COLUMN months varchar(20);

-- 5.
UPDATE customer_loyalty_history
SET enrollment_month = CASE
							WHEN enrollment_month = 1 THEN 'January'
							WHEN enrollment_month = 2 THEN 'February'
							WHEN enrollment_month = 3 THEN 'March'
							WHEN enrollment_month = 4 THEN 'April'
							WHEN enrollment_month = 5 THEN 'May'
							WHEN enrollment_month = 6 THEN 'June'
							WHEN enrollment_month = 7 THEN 'July'
							WHEN enrollment_month = 8 THEN 'August'
							WHEN enrollment_month = 9 THEN 'September'
							WHEN enrollment_month = 10 THEN 'October'
							WHEN enrollment_month = 11 THEN 'November'
							WHEN enrollment_month = 12 THEN 'December'
						ELSE enrollment_month
END;

UPDATE customer_loyalty_history
SET cancellation_month = CASE 
							WHEN cancellation_month = 1 THEN 'January'
							WHEN cancellation_month = 2 THEN 'February'
							WHEN cancellation_month = 3 THEN 'March'
							WHEN cancellation_month = 4 THEN 'April'
							WHEN cancellation_month = 5 THEN 'May'
							WHEN cancellation_month = 6 THEN 'June'
							WHEN cancellation_month = 7 THEN 'July'
							WHEN cancellation_month = 8 THEN 'August'
							WHEN cancellation_month = 9 THEN 'September'
							WHEN cancellation_month = 10 THEN 'October'
							WHEN cancellation_month = 11 THEN 'November'
							WHEN cancellation_month = 12 THEN 'December'
						ELSE 'Active'
END;

UPDATE customer_flight_activity
SET months = CASE 
							WHEN months = 1 THEN 'January'
							WHEN months = 2 THEN 'February'
							WHEN months = 3 THEN 'March'
							WHEN months = 4 THEN 'April'
							WHEN months = 5 THEN 'May'
							WHEN months = 6 THEN 'June'
							WHEN months = 7 THEN 'July'
							WHEN months = 8 THEN 'August'
							WHEN months = 9 THEN 'September'
							WHEN months = 10 THEN 'October'
							WHEN months = 11 THEN 'November'
							WHEN months = 12 THEN 'December'
						ELSE months
END;
-- 6.
ALTER TABLE customer_loyalty_history
ALTER COLUMN cancellation_year varchar(50);
-- 7.
UPDATE customer_loyalty_history
SET cancellation_year = 'Active'
WHERE cancellation_year IS NULL;

UPDATE customer_loyalty_history
SET cancellation_month = 'Active'
WHERE cancellation_month IS NULL;
-- 8.
ALTER TABLE customer_flight_activity
ALTER COLUMN loyalty_number int NOT NULL;

ALTER TABLE customer_flight_activity
ADD CONSTRAINT fk_loyalty_number
FOREIGN KEY (loyalty_number)
REFERENCES customer_loyalty_history(loyalty_number);

```

# Testing 

Here are the data quality tests conducted:

## Row count check
```sql
/*
# Count the total number of records (or rows) 
*/
SELECT
    COUNT(*) AS no_of_rows
FROM
    customer_loyalty_history;

SELECT
    COUNT(*) AS no_of_rows
FROM
    customer_flight_activity;
```

![Row count check](assets/images/1_row_count_check.png)



## Column count check
### SQL query 
```sql
/*
# Count the total number of columns (or fields) are in the SQL view
*/


SELECT
    COUNT(*) AS column_count
FROM
    INFORMATION_SCHEMA.COLUMNS
WHERE
    TABLE_NAME = 'customer_loyalty_history'


SELECT
    COUNT(*) AS column_count
FROM
    INFORMATION_SCHEMA.COLUMNS
WHERE
    TABLE_NAME = 'customer_flight_activity'


```
### Output 
![Column count check](assets/images/2_column_count_check.png)



## Data type check
### SQL query 
```sql
*/
	SELECT
    COLUMN_NAME,
    DATA_TYPE
FROM
    INFORMATION_SCHEMA.COLUMNS
WHERE
    TABLE_NAME = 'customer_flight_activity';
	SELECT
    COLUMN_NAME,
    DATA_TYPE
FROM
    INFORMATION_SCHEMA.COLUMNS
WHERE
    TABLE_NAME = 'customer_loyalty_history';
```
### Output
![Data type check](assets/images/3_data_type_check.png)


## Duplicate count check
### SQL query 
```sql
/*
# Check for duplicate rows in the view
WITH CTE AS (
    SELECT *,
           ROW_NUMBER() OVER (PARTITION BY loyalty_number, year, months, flights_booked, flights_with_companions, total_flights, distance, points_accumulated, points_redeemed, dollar_cost_points_redeemed ORDER BY loyalty_number) AS rn
    FROM customer_flight_activity
)
select count (*) as duplicate_count FROM CTE
WHERE rn > 1;
```
### Output
![Duplicate count check](assets/images/4_duplicate_records_check.png)

# Visualization 


## Results

- What does the dashboard look like?

![GIF of Power BI Dashboard](assets/images/top_uk_youtubers_2024.gif)

This shows the Top UK Youtubers in 2024 so far.













Issues
-no dataset showing flight bookings or churn rates from earlier ye
-sakary issurs
