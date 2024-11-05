# Lita-Capstone-Project-2
## Project Work for incubator hub data analysis training 
### Project Topic - Customer Segmentation for a Subscription Service


### Project Objectives
This project involves analyzing customer data for a subscription service to identify segments and trends. The goal is to understand 
- customer behavior,
- track subscription types, and
- identify key trends in cancellations and renewals.

### Scope:
This project will focus on Analysing subscription pattern data from **Q1 2022 to Q3 2023.** Covering:

- Sales transactions
- Subsription Cancelation Patterm
- Subsription types (Basic, Standard and Premium)
- Store locations (Nouth, East, West and South)


### Methodology:
1. **Data Collection:** A documented Excel file - LITA Capstone Dataset.xlsx
2. **Data Cleaning and preprocessing:** Ensure data accuracy and consistency use analysis tools (Excel and Power BI), through the following steps
   - Data loading and inspection
3. **Handing Missing Variables:** Like editing some columns to make it compartible with SQL SERVER
4. **Data Cleaning and formatting**
5. **Data Ananlysis:** Apply data vitualisation techniques using analysis tools such as (Excel and Power BI)
6. **Data Querying:** querying data to extract key insights using SQL (Structutred Query Language) with the aid of SQL Server.
7. **Findings and Recommendation**
  
### Expected Outcomes:
1. A comprehensive susbscription pattern analysis report highlighting trends and opputunities.
2. Data-Driven recommendations to improve revenue and subscription trends


### Deliverables:
1. **Data Analysis**
Some Basic lines of Code - excel functions, SQL queries and Some DAX expression used during analysis Excel functions

Excel PIVOT TABLES and CALCULATIONS

![sub pivot 1](https://github.com/user-attachments/assets/84e41da7-17d1-4ca6-a55b-6331086a2831)

![sub pivot 2](https://github.com/user-attachments/assets/56fbd119-18ae-40ee-ac91-1e6280bf43c7)

![sub pivot 3](https://github.com/user-attachments/assets/f96fdcb0-deaf-4066-8bba-91106aa1ae76)

![sub pivot 4](https://github.com/user-attachments/assets/cffbd812-bbe9-4cac-b17f-59ed603d7ca1)

![sub pivot 5](https://github.com/user-attachments/assets/0a9e484c-de26-4815-bb48-90f3d6e75686)

![sub pivot 6](https://github.com/user-attachments/assets/acdc5652-9a0d-4753-abcc-e4712cbdfa6d)

![sub pivot 7](https://github.com/user-attachments/assets/6bebd28d-744f-4682-a502-ff578bdeccc1)

![sub pivot 8](https://github.com/user-attachments/assets/83cb5f39-7e49-421e-9bb9-d95653031307)




**SQL QUERIES**
 
  ~~~
  SELECT * FROM [dbo].[LITA Capstone SUBSRIPTION DATA];
~~~

------- RETRIEVE THE TOTAL NUMBER OF CUSTOMERS FROM EACH REGION------

~~~
SELECT 
Region,
COUNT(CustomerID) AS total_customers
FROM
[dbo].[LITA Capstone SUBSRIPTION DATA]
GROUP BY
Region
ORDER BY
total_customers DESC;
~~~


------- MOST POPULAR SUBSCRIPTION TYPE BY NUMBER OF CUSTOMERS-------
~~~
SELECT
SubscriptionType,
COUNT(CustomerID) AS total_customers
FROM 
[dbo].[LITA Capstone SUBSRIPTION DATA]
GROUP BY 
SubscriptionType
ORDER BY
total_customers DESC;
~~~

------- CUSTOMERS WHO CANCELLED THEIR SUBSCRIPTION WITHIN 6 MONTHS--------
~~~
SELECT CustomerID, CustomerName,SubscriptionType,SubscriptionStart,SubscriptionEnd,
DATEDIFF(MONTH, SubscriptionStart, SubscriptionEnd) AS subscription_duration
FROM
[dbo].[LITA Capstone SUBSRIPTION DATA]
WHERE 
Canceled = 1
AND DATEDIFF(MONTH,SubscriptionStart, SubscriptionEnd) <=6;
~~~


-------- AVERAGE SUBSCRIPTION DURATION FOR ALL CUSTOMER---------
~~~
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
~~~

-------- CUSTOMERS WITH SUBSCRIPTION LONGER THAN 12 MONTH----------
~~~
SELECT CustomerID, CustomerName,SubscriptionType,SubscriptionStart,SubscriptionEnd,
DATEDIFF(MONTH,SubscriptionStart,SubscriptionEnd) AS sub_durationMonth
FROM
[dbo].[LITA Capstone SUBSRIPTION DATA]
WHERE
DATEDIFF(MONTH, SubscriptionStart, SubscriptionEnd) > 12
ORDER BY
sub_durationMonth DESC;
~~~

---------- TOTAL REVENUE BY SUBSCRIPTION TYPE----------
~~~
SELECT
SubscriptionType,
SUM(Revenue)  AS total_revenue
FROM
[dbo].[LITA Capstone SUBSRIPTION DATA]
GROUP BY
SubscriptionType
ORDER BY
total_revenue DESC;
~~~

---------- TOP 3 REGION BY SUBSCRIPTION CANCELATIONS---------
~~~
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
~~~


---------	TOTAL NUMBER OF ACTIVE AND CANCELED SUBSCRIPTION----------
~~~
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
~~~
**Power BI Virtualization**

<img width="484" alt="Customerdata" src="https://github.com/user-attachments/assets/00543ad9-4cd9-4fda-b7ed-8a1d7d234154">


### Recommendations
After a thorough data analysis of Subscription data, here are some recommendations:

- Non of the subscribers in the Eastern region canceled their service, the company might want to find out its strategy in that region, then implementing it in other regions.
- Likewise, the company could increase its market strategies for Basic subscription type, since it contributed larger percent of the overall Revenue.
- The company could also identify gaps in product offering. Like for the last quarter of 2023, **Premium** recorded no active subscriber.

### Timeline:
- Data analysis:
- Findings and recommendations:
- Report and presentation preparation:


### Project Team:
**Data Analyst:** Ikupoluyi Justina
