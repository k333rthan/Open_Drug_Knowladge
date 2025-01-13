# Open Drug Knowladge Analysis
Helps to Analyse on the drugs, price, type, products etc from the given relational database dataset

## Project Overview

The primary objective of this project is to analyze the pricing, distribution, and trends of drugs across various stores using the provided dataset. By leveraging SQL, we aim to gain actionable insights into drug pricing patterns, store performance, and product availability, which can aid decision-making in the pharmaceutical industry.

## Dataset Description
Some of the important columns for the Data Analysis are listed below: 

- id: Unique identifier for each record (Primary Key).
- product_id: ID representing a specific drug.
- store_id: ID representing the store offering the drug.
- type: Type of listing (e.g., COUPON).
- price: Price of the drug.
- url: Link to the product's coupon or detailed page.

## Price Insights

- Analyze the average, minimum, and maximum price of drugs.
- Identify the cheapest and most expensive stores for specific products.
- Detect significant price variations for the same drug across different stores.


## Store Performance

- Determine which stores have the highest number of drug listings.
- Identify the stores offering the most "COUPON" type products.
- Analyze the average price trends across stores to rank them by affordability.

## Product Trends

- Explore the distribution of product listings across stores.
- Identify products with the highest and lowest price ranges.
- Detect popular products with frequent listings in multiple stores.
- URL-Based Analysis

## SQL Query Documentation
- Price Analysis of the products
- Store Analysis across various pharmacies
- Product trends showcasing the variation among the products, stores, prices etc

## Proposed SQL Queries

#### Price Analysis

What is the top 10 highest average price of drugs across all stores?
```
select avg(p.price) as 'Average price', s.name from price p left join store s 
on s.id=p.id 
group by s.name
order by avg(p.price) desc
limit 10  offset 1;
```
Which store offers the lowest average price for a specific drug?
```
select avg(p.price) as 'Average Price', d.name as 'drug name', s.name as 'store name'
from price p join treatment t
on p.id=t.id
join store s 
on p.id=s.id
join drug d on d.id=t.drug_id
group by s.name, d.name
order by avg(p.price) desc
```
Which products have prices greater than $80?
```
SELECT d.name, p.price from product pr 
join price p on p.id=pr.id
join drug d on d.id=pr.drug_id
WHERE p.price > 80
order by p.price desc;
```
#### Store Insights

Which store has the highest number of drug listings?
```
select count(d.id), s.name as ' Store Name' from drug d left join treatment t
on d.id=t.drug_id
join store s on t.id=s.id
group by s.name
```
What is the average price for each product across all stores?
```
SELECT d.name , round(AVG(pr.price),2) AS average_price
FROM product p join price pr
on p.id=pr.id
join drug d on d.id=p.drug_id
GROUP BY d.name
order by average_price desc
```
Which stores offer the highest number of "COUPON" type drugs?
```
SELECT s.name, COUNT(p.type) AS coupon_count
FROM store s join price p
on p.id=s.id
WHERE p.type = 'COUPON'
```
#### Product Trends
Which products have the highest average price across all stores?
```
SELECT d.name, round(AVG(p.price),2) AS average_price
FROM price p join product pr 
on pr.id=p.id
join drug d on pr.drug_id=d.id 
GROUP BY d.name
ORDER BY average_price DESC
LIMIT 5;
```
Which products have the same price across all stores?
```
SELECT d.name 
FROM product pr join price p
on p.id=pr.id
join drug d on d.id=pr.drug_id
GROUP BY d.name
HAVING MAX(p.price) = MIN(p.price);
```
## Visualizations ###(e.g., price trends, top stores) created using Power BI for better decision-making.
![image alt](https://github.com/k333rthan/Open_Drug_Knowladge/blob/main/Screenshot%202025-01-13%20210804.png?raw=true)

The above report shows :
  1. Average Drug Price by Store (Bar Chart)
	Visualize the average price of drugs across different stores.
	2.	Drug Price Distribution by Price Type (Pie Chart)
	Show the percentage of drugs sold under different price types (e.g., Coupon, Cash, Gold).
	3. Top 10 Most Expensive Drugs (Column Chart)
	Highlight the top 10 drugs with the highest average price.
	4.	Price Range of Drugs by Store (Box and Whisker Plot)
	Display the minimum, maximum, and average drug prices for each store.
  5. Number of stores and the Sum of Prices Card chart





![image alt](https://github.com/k333rthan/Open_Drug_Knowladge/blob/main/Screenshot%202025-01-13%20210730.png?raw=true)



The above image only focuses on the  selected pharmacy and highlights the data related to the purticular pharmacy (here, CVS Pharmacy)

## Data Insights Report

Comprehensive report summarizing pricing trends, store performance, and product distribution.
Interactive Dashboards




Recommendations

Suggestions for optimizing pricing strategies and improving product availability based on the analysis.
Potential Applications
Price comparison tools for consumers.
Strategic pricing for pharmaceutical companies.
Store benchmarking for competitive analysis.








