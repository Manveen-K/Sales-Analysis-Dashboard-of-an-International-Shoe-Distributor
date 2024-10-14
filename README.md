# Sales Analysis Dashboard for a Leading International Shoe Distributor
This data analysis project involved creating a comprehensive dashboard using Power BI to analyse sales data for a leading international shoe distributor.

### Dashboard Link: 
[Sales Dashboard for a Leading International Shoe Distributor](https://app.powerbi.com/view?r=eyJrIjoiN2MwMWExZmItN2FkMy00ZmRmLWFiMDQtOWEyN2FiN2I5NmM5IiwidCI6Ijg5OWM1ZDljLTVmMjUtNDFmZS05YWVjLTdjYWI1MGY4YTQ4ZiJ9)


![Dashboard](https://github.com/user-attachments/assets/08c79db5-cb87-4d80-8736-5017d26f395a)


## Table of Contents:
- [Problem Statement](#problem-statement)
- [Data Source](#data-source)
- [Tools](#tools)
- [Assumptions](#assumptions)
- [Steps Followed](#steps-followed)
- [Insights](#insights)
- [Recommendations](#recommendations)

## Problem Statement
As a leading international shoe distributor, the company wants to gain actionable insights into its sales performance across diverse regions, product categories, and sales channels. The primary objective is to direct focus towards high-performing products, optimizing customer satisfaction, and ensuring revenue maximization. 

## Data Source
Sales Data: The primary dataset used for this analysis is the "Sales Dataset.xlsx" file, containing 8 sheets namely -  sales data, product details, location details, discount details, sales channel details, channel type details, sales target, and complaints & returns. Another sheet called "Date Master" was made for the purpose of building model and connecting all the necessary sheets with each other.

## Tools
1. Excel
2. PowerBI 

## Assumptions
1. All provided data is accurate and up-to-date.
2. The sales targets are set based on historical trends and market analysis.
3. Complaints and returns data reflect customer satisfaction and product quality issues.
4. The company's primary objective is to maximize profit while maintaining customer satisfaction.
5. The assumption is made that the "Sales Channel" and "Channel Type" sheets follow a hierarchical structure, where "Channel Type" represents broader categories and "Sales Channel" represents specific subcategories under each type.
6. Since the Products Returned column has continous values, so we have considered it as the average number of products returned in that entire month.

## Steps Followed

#### Step 1: Data Loading and Cleaning
- The data was loaded into Power BI Desktop from eight Excel sheets containing sales data, product details, location details, discounts, sales channels, sales targets, and complaints and returns.
- It was observed that data did not had any null values or duplicate records.

#### Step 2: Data Modelling
- In the model view, it was observed that two files, "sales target" and "complaints and returns", were not connected to the fact table (sales data).
- It was because the common column for connection was the date column, but the two files (sales target and complaints and returns) only contained month-end dates, resulting in incomplete connections.
- To address this issue, a date master sheet was created containing all the dates and was connected to the fact table.
- Sales target and complaints and returns were then connected to the date master sheet, establishing a snowflake schema to ensure comprehensive data integration.
  
![Model View](https://github.com/user-attachments/assets/bc9d1843-80b6-424b-9628-38a1508d38e1)


#### Step 3: Identification and calculation of meaningful Business Metrics using DAX 

- The following Calculated Columns were created:
  1. Total Sales After Discount
     ```DAX
      'Sales Data'[Total Sales]-('Sales Data'[Total Sales]* 'Sales Data'[Discount])
     ```
  2. Total Profit/Loss
     ```DAX
      'Sales Data'[Total Sales after discount]-'Sales Data'[Total Cost]
     ```
  3. Profit Margin
     ```DAX
      ('Sales Data'[profit/loss]/'Sales Data'[Sum Total Sales after Discount])*100
     ```
  4. Return Rate
      ```DAX
      ('Complaints & Returns'[Products Returned]/'Complaints & Returns'[Products Sold])*100
     ```

- The following Calculated Measures were created:
  1. Average Profit Margin
     ```DAX
      AVERAGE('Sales Data'[Profit Margin])
     ```
  2. Average order value
     ```DAX
       'Sales Data'[Sum Total Sales after Discount]/'Sales Data'[Total Number of Customers]
     ```
  3. ⁠Average return rate
     ```DAX
       AVERAGE('Complaints & Returns'[Return Rate])
     ```
  4. ⁠Average revenue per product
     ```DAX
        DIVIDE([Sum Total Sales after Discount],SUM('Sales Data'[Quantity]))
     ```
  5. ⁠CSAT - Customer Satisfaction Score
     ```DAX
         'Sales Data'[Sum Total of Customer Rating]/8044
     ```
  6. Sum Total of Customer Rating
     ```DAX
         SUM('Sales Data'[Customer Rating])
     ```
  7. Sum Total Sales after Discount
     ```DAX
          SUM('Sales Data'[Total Sales after discount])
     ```
  8. ⁠Total Number of Customers (this helped in understanding the total number of new customers)
     ```DAX
          Count('Sales Data'[Customer Type])
     ```
 
#### Step 4: Dashboard Design
- The dashboard is a multipage one with three views: Overview, Product Centric, and Customer Centric.
- Three filters were created for Year, Continent, and Product Class, which were made available on all three views to enable dynamic filtering.
- Cards were incorporated to depict key business metrics, such as:
  - Average Profit Margin
  - Number of New customers gained
  - Average revenue per product
  - Average order value
  - Average return rate
  - Number of Complaints 
  - Customer satisfaction score
- Visualisation such as Map, KPI visual, stacked bar charts, bubble plot, line chart have been used to depict the data perfectly.
- Also, Rose Chart has been used from the added visual called "Aster Plot 1.4.0) to depict top 5 selling products.
  

<img width="280" alt="Total Sales by Name" src="https://github.com/user-attachments/assets/7870da8c-2ee5-4ce7-9f6d-a878b0eac300">


#### Step 5: Dashboard Navigation
- The dashboard contains three buttons to allow toggling between the three pages (Overview, Product Centric, and Customer Centric).
- This navigation feature enhances user experience and facilitates seamless exploration of different aspects of the data analysis.
  
<img width="554" alt="Sales Dashboard" src="https://github.com/user-attachments/assets/10e1ba4c-4b1e-4222-b9d4-89075ea9d0b0">

## Insights
Following inferences can be drawn from the dashboard:

- The company achieved $5.64 million in sales from 2017 to 2020, exceeding the original target by 510.39%.
- Sales targets were successfully achieved each year, demonstrating consistent performance and strategic execution.
- However, the sales target was not achieved for the Deluxe Product class in any of the years.
- Additionally, the sales target was not achieved for the Standard Product class in 2017 and 2020.
- The United States consistently emerged as the top-profit generating country, followed by Switzerland, China, Australia, and Singapore.
- The top 5 most selling products are: H > C > B > E > F. These products have remained as top selling for almost all the years.
- Product H of Brand C has been responsible for the maximum sales over the entire course of 4 years.
- In 2017, Deluxe Product class did not exit.  It was in 2018, that product J was introduced in the deluxe class, and it was only in 2020, when products O, P, T were launched, and product P can be considered as an instant hit as it was one of the top selling products in the year 2020.
- Product Q was launched in 2020 itself under the elite product class, and it was the highest selling product in 2020.
- Both "Average revenue per product" and "Average Order Value" are the highest for Elite product class.
- Average Profit Margin is highest for the Standard Product Class.
  
#### Product Centric:
- Sports shoes have been consistently the highest-selling shoes, except for 2017 when gym shoes were the most popular, though gym shoe sales have declined since then.
- Sales of sports shoes showed a progressive ascent percentage of 104.10% from 2017 to 2018 and reached a noteworthy peak at 1.3M in 2019.
- Formal shoes unexpectedly emerged as the second-highest selling product category in 2020.
- Indoor shoes started gaining popularity in 2018, suggesting evolving consumer trends and preferences.
- The Standard product class had the highest profit margin, with Product R achieving the highest profit margin within this class.
- Product K of Brand C had the highest Average Revenue per Product (ARPP)
- 2019 was the most profitable year overall, except for the Deluxe product class, which recorded its lowest profit during that year.
- Profit trends varied across regions, with Oceania and America experiencing a sharp dip in profit from 2019 to 2020, while Asia and Europe saw significant increases during the same period.
- Brand C remained the top-selling brand consistently, reflecting its strong market presence and consumer appeal.
- Brand A experienced significant growth from 2019 to 2020, while other brands witnessed a decline.
- In Europe, Brand C's popularity increased steadily over the years, indicating successful brand management and marketing strategies.
- Company is getting most sales through Paid Ads, and in that too, online channel is generating the highest sales. 
- The Sales through Blogs have increased throughout the four years, it jumped by 151.02% from 2017 to 2020,  highlighting the effectiveness of this marketing channel.

#### Consumer Centric:
- Return rate has seen a decline from 2017 to 2019, but a sudden increase has been observed in 2020.
- Delivery issues are the primary reason for complaints, accounting for 28.9%, followed closely by packaging issues at 25.58%.
- Sports shoes constitute a significant portion (42.84%) of total complaints, with delivery issues being the primary grievance at 30.8%.
- Damaged product receipt is a major complaint reason within the sports shoe category.
- Standard sports shoes by Brand A have the highest number of complaints, with over 50% directly related to manufacturing and packaging issues.
- Customer satisfaction scores increased over the years but decreased in 2020
- The premium class garnered the most new customers and achieved the highest customer satisfaction score.
- In Asia, damaged products emerged as a significant concern for customers, surpassing delivery issues in complaint frequency.


## Recommendations

#### 1. New Delivery Partners
- One of the biggest complaint reasons amongst each product category are delivery issues. Europe being the highest contributor at 42.11%. Therefore we would recommend looking into different delivery partners who can reduce the rate of delivery complaints.

#### 2. Sales Target Alignment
- Company should review and adjust sales targets for the Deluxe and Standard Product classes to ensure they are realistic and achievable.

#### 3. Online Channels to Sell Products
- The highest performing sales channel is Online within which the highest channel type is Paid Ads. Therefore we would like to suggest selling underperforming products and new products using paid ads.

#### 4. Market Analysis 
- Company should continue prioritizing markets with high-profit potential, such as the United States, Switzerland, China, Australia, and Singapore.
- Oceania is the least performing region in terms of sales as well as the number of customer. Only 10 percent of total new customers come from this region. So we would suggest a proper analaysis of the footwear industry in this region.

#### 5. Customer Satisfaction and retention
- Company can implement quality control measures to minimize damaged product receipt, especially within the sports shoe category.




