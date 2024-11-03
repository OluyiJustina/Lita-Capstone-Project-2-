# Lita-Capstone-Project-2
## Project Work for incubator hub data analysis training 
### Project Topic - Customer Segmentation for a Subscription Service


### Project Objectives
This project involves analyzing customer data for a subscription service to identify segments and trends. The goal is to understand 
- customer behavior,
- track subscription types, and
- identify key trends in cancellations and renewals.

### Scope:
This project will focus on Analysing sbscription pattern data from Q1 2022 to Q3 2023. Covering:

Sales transactions
Subsription Cancelation Patterm
Subsription types (Basic, Standard and Premium)
Store locations (Nouth, East, West and South) 
  
  
  
  QUERIES
 
  
  ~~~SELECT * FROM [dbo].[LITA Capstone SUBSRIPTION DATA];

------- RETRIEVE THE TOTAL NUMBER OF CUSTOMERS FROM EACH REGION------
SELECT 
Region,
COUNT(CustomerID) AS total_customers
FROM
[dbo].[LITA Capstone SUBSRIPTION DATA]
GROUP BY
Region
ORDER BY
total_customers DESC;

------- MOST POPULAR SUBSCRIPTION TYPE BY NUMBER OF CUSTOMERS-------

SELECT
SubscriptionType,
COUNT(CustomerID) AS total_customers
FROM 
[dbo].[LITA Capstone SUBSRIPTION DATA]
GROUP BY 
SubscriptionType
ORDER BY
total_customers DESC;


------- CUSTOMERS WHO CANCELLED THEIR SUBSCRIPTION WITHIN 6 MONTHS--------

SELECT CustomerID, CustomerName,SubscriptionType,SubscriptionStart,SubscriptionEnd,
DATEDIFF(MONTH, SubscriptionStart, SubscriptionEnd) AS subscription_duration
FROM
[dbo].[LITA Capstone SUBSRIPTION DATA]
WHERE 
Canceled = 1
AND DATEDIFF(MONTH,SubscriptionStart, SubscriptionEnd) <=6;



-------- AVERAGE SUBSCRIPTION DURATION FOR ALL CUSTOMER---------

SELECT
AVG(DATEDIFF(DAY,SubscriptionStart,SubscriptionEnd)) AS
average_durationDay,
AVG(DATEDIFF(MONTH, SubscriptionStart, SubscriptionEnd)) AS
average_durationMonth,
AVG(DATEDIFF(YEAR, SubscriptionStart, SubscriptionEnd)) AS
average_durationYear
FROM
[dbo].[LITA Capstone SUBSRIPTION DATA]
WHERE
Canceled = 1;

-------- CUSTOMERS WITH SUBSCRIPTION LONGER THAN 12 MONTH----------

SELECT CustomerID, CustomerName,SubscriptionType,SubscriptionStart,SubscriptionEnd,
DATEDIFF(MONTH,SubscriptionStart,SubscriptionEnd) AS sub_durationMonth
FROM
[dbo].[LITA Capstone SUBSRIPTION DATA]
WHERE
DATEDIFF(MONTH, SubscriptionStart, SubscriptionEnd) > 12
ORDER BY
sub_durationMonth DESC;

---------- TOTAL REVENUE BY SUBSCRIPTION TYPE----------

SELECT
SubscriptionType,
SUM(Revenue)  AS total_revenue
FROM
[dbo].[LITA Capstone SUBSRIPTION DATA]
GROUP BY
SubscriptionType
ORDER BY
total_revenue DESC;


---------- TOP 3 REGION BY SUBSCRIPTION CANCELATIONS---------

SELECT TOP 3
Region,
COUNT(CustomerID) AS cancelled_count
FROM
[dbo].[LITA Capstone SUBSRIPTION DATA]
WHERE
Canceled = 1
GROUP BY 
Region
ORDER BY
cancelled_count DESC;

---------	TOTAL NUMBER OF ACTIVE AND CANCELED SUBSCRIPTION----------

SELECT
SUM(CASE WHEN 
Canceled = 0 
THEN 1
ELSE 0 END) AS Active_subs,
SUM(CASE 
WHEN Canceled = 1 
THEN 1 
ELSE 0 END)AS cancelled_subs
FROM
[dbo].[LITA Capstone SUBSRIPTION DATA];
