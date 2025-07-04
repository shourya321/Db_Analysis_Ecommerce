# Elist E-Commerce Analysis: 2019-2022

<img width="750" alt="Tableau dashboard showing tables, line graphs, and area charts for total sales, total orders, and average time to ship" src="https://imgur.com/DpPG33J.png">

Analyzing Elist order trends from 2019-2022. An interactive Tableau dashboard can be found [here](https://public.tableau.com/app/profile/sean.atkinson/viz/ElistOrdersDashboard_16896324404540/ordersdashboard).

# Table of Contents
<a id='table_of_contents'></a><br>
[Project Summary](#section_1)<br>
[Part 1: Trends (Excel)](#section_2)<br>
[Part 2: Targeted Insights (SQL)](#section_3)<br>
[Part 3: Visualizations (Tableau)](#section_4)<br>
[Part 4: Recommendations & Next Steps](#section_5)<br>
[Addendum: Notes on Data Cleaning](#section_6)<br>

<a id='section_1'></a>
# Project Summary
Elist is a demo e-commerce platform specializing in global sales of trending electronic gadgets.

In this project, I analyzed a dataset to investigate trends and growth rates in revenue, average order value (AOV), product popularity, marketing channels, refund rates, and shipping efficiency. Additionally, I closely examined their recently launched loyalty program to assess its effectiveness in overall sales, AOV, and total orders.

This project consists of four parts:
- <b>Part 1: Trends</b>
  * Using Excel, I take a high-level look at some of the broad trends within the data to see what notable insights can be pulled out for the finance and product team.
- <b>Part 2: Targeted Insights</b>

  * With the aid of SQL, I pull out more targeted insights for the finance and marketing team, highlighting things like MacBook sales, refund rates, and best performing marketing channels.

- <b>Part 3: Visualizations</b>
  * Leveraging Tableau, I create a dashboard for the finance and product teams (as well as the sales and operations teams to a lesser extent) to monitor metrics of interest on an ongoing basis.

- <b>Part 4: Recommendations & Next Steps</b>
  * Suggestions on things to take a look at going forward.

The data I'll be using is spread out across four tables and consists of information on orders, order statuses, customers, and geographic information.

Here is the Entity Relationship Diagram:

<img width="750" alt="Entity Relationship Diagram showing orders, order statuses, customers, and geographic information tables" src="https://imgur.com/L3Fh37t.png">

You can view the data in greater detail [here](https://github.com/sean-atkinson/elist_ecommerce_analysis/tree/main/data).
<a id='section_2'></a>
# Part 1: Trends (Excel)
[(Back to table of contents)](#table_of_contents)<br><br>
<b>Summary of Trends</b>:

<b>Yearly</b>
- Interestingly, the first year of the pandemic (2020) saw the highest average order value of $298.
- Total orders were down to 19K in 2022 (from 31k in 2021).
- Revenue was down 44% year-over-year in 2022.
-  The concerning sales numbers of 2022 appear to reflect broader trends in the e-commerce industry. Factors such as the economic recession, an oversaturated market, decreased effectiveness of marketing campaigns, and supply chain issues were [identified by Statista](https://www.statista.com/chart/27982/e-commerce-revenue-and-forecasts/?ssp=1&setlang=en-CA&safesearch=moderate) as contributors to an unprecedented forecasted shrink in e-commerce revenue for 2022. Particularly notable were changes in digital marketing practices: [the privacy update in Apple's iOS 14.5, alongside a 47% increase in Facebook advertising costs](https://www.forbes.com/sites/forbestechcouncil/2022/03/14/e-commerce-trends-2022-what-the-future-holds/?ssp=1&setlang=en-CA&safesearch=moderate&sh=6ca444d258da), seems to have had a profound impact on e-commerce merchants.

<b>Seasonality</b>
- Winter and spring tend to perform better, most likely due to holiday sales and special promotions.
- There's a noticeable sales uptick in the first half of 2020, most likely due to the pandemic.

<b>Products</b>
- Airpods have consistently been our best-selling product in terms of total orders. 
- In 2022, Airpods and a gaming monitor made up a whopping 68% of all orders.
- Bose Soundsport Headphones have consistently performed poorly. We've only sold 25 pairs over 3 years.

<b>Loyalty Program</b>
- We recommend continuing to expand this. When the program started in 2019, members were spending an average of $29 less than non-members. In 2022, loyalty program members now spend an average of $34 more than non-members per purchase.
- By the end of 2022, loyalty program members generated 27% more revenue compared to non-members. This is largely attributed to their higher receptiveness to our marketing efforts. The fact that they are loyalty members makes them more open to receiving emails from us, as demonstrated by spending 217% more than non-members through that channel in 2022. It's worth noting that email marketing boasts a [47x ROI](https://cxl.com/blog/email-marketing-strategy/) and has remained relatively unaffected by changes in the marketing landscape.<br>


<b>Technical Analysis:</b><br>
For this section, I used Pivot Tables, conditional formatting, aggregation functions, and statistical analysis to clean, analyze, and summarize my insights for the finance and product teams.

Here is an example of the pivot table used for seasonality insights:

<img width="750" alt="Excel pivot table showing totals and growth rates for monthly sales, AOV, and orders" src="https://imgur.com/Uns8sPD.png">

You can find more detailed analysis in [this downloadable Excel workbook](https://github.com/sean-atkinson/elist_ecommerce_analysis/blob/main/excel/elist_orders_case_study.xlsx).

<a id='section_3'></a>
# Part 2: Targeted Insights (SQL)
[(Back to table of contents)](#table_of_contents)<br><br>
<b>Summary of Targeted Insights</b>:

<b>North American MacBook sales (all year)</b>
- Average of 30 units sold per month.
- Average monthly sales are $47.8K.

<b>Refund rates</b>
- For 2020, the monthly refund rate was 3.1%.
- In 2021, the lowest amount of returns for Apple products was 6 (in November). The highest was 33 (in March).
- Across all years, Macbook Airs had the highest refund rate at 4.2% followed by ThinkPads (3.8%) and iPhones (3.5%).

<b>Account creation methods (Jan-Feb 2022)</b>
- Accounts created on tablets had the highest average order value at $287 (but only 25 purchases were made on tablets).
- Desktop was the account creation method that led to the most new customers, with 2,487, which is more than three times the number of new customers generated by the next closest method, mobile, with 701.

<b>Time to purchase (all years)</b>
- Average of 51 days between account creation and first purchase.

<b>Marketing channels (all years)</b>
- Direct - highest number of orders.
- Emails - second highest number of orders.

<b>Technical Analysis:</b><br>
For this analysis, I used SQL and BigQuery. In regards to SQL, I used aggregation functions, window functions, joins, filtering, CASE expressions, common table expressions (CTEs), and in a couple instances the QUALIFY clause to use row_number() to filter results.

You can find my SQL queries [here](https://github.com/sean-atkinson/elist_ecommerce_analysis/blob/main/sql/elist_sales_trends_queries.sql).

Here is an example of a query result that uses the aforementioned qualify clause:
```sql
-- Creating a brand category and totaling the amount of refunds per month
-- Filtering to the year 2020
WITH highest_num_refunds_cte AS (
    SELECT
        CASE
            WHEN LOWER(orders.product_name) LIKE '%apple%' OR LOWER(orders.product_name) LIKE '%macbook%' THEN 'Apple'
            WHEN LOWER(orders.product_name) LIKE '%samsung%' THEN 'Samsung'
            WHEN LOWER(orders.product_name) LIKE '%thinkpad%' THEN 'ThinkPad'
            WHEN LOWER(orders.product_name) LIKE '%bose%' THEN 'Bose'
            ELSE 'Unknown'
        END AS brand,
        DATE_TRUNC(order_status.refund_ts, MONTH) AS month,
        COUNT(order_status.refund_ts) AS num_refunds
    FROM 
        elist.orders AS orders 
    JOIN 
        elist.order_status AS order_status 
    ON 
        orders.id = order_status.order_id
    WHERE 
        EXTRACT(YEAR FROM order_status.refund_ts) = 2020
    GROUP BY 
        1, 2
)
-- Getting the highest month and corresponding number of refunds for each brand in 2020 
SELECT
    brand, 
    month, 
    num_refunds
FROM 
    highest_num_refunds_cte
QUALIFY 
    ROW_NUMBER() OVER (PARTITION BY brand ORDER BY num_refunds DESC) = 1
ORDER BY 
    1;
```
And here is its result:
| brand    | month      |   num_refunds |
|:---------|:-----------|--------------:|
| Apple    | 2020-06-01 |            56 |
| Samsung  | 2020-04-01 |             7 |
| ThinkPad | 2020-04-01 |             9 |
| Unknown  | 2020-05-01 |            25 |



<a id='section_4'></a>
# Part 3: Visualizations (Tableau)
[(Back to table of contents)](#table_of_contents)<br><br>

<b>Summary of Insights:</b>

<b>Orders</b>
- Airpods, gaming monitors, and charging packs have accounted for over 80% of all orders from 2019-2022.
- Every product except webcams saw its total orders peak around the start of the pandemic. Paradoxically, total orders for webcams rose in the following years. This is something we should investigate further.

<b>Shipping times</b>
- iPhones and Bose headphones have, relative to all other products, incredibly high variability when it comes to shipping times. One might wonder if this is a chicken and egg situation, considering their sales. Are the shipping times for iPhones and Bose headphones all over the place because we rarely sell them (and consequently don't have much stock on hand)? Or do we rarely sell iPhones and Bose headphones because customers find our shipping times to be too unpredictable?  

<b>Sales</b>
- From 2019-2022, gaming monitors have consistently generated the highest total sales revenue, with the exception of a brief period at the end of 2020.
- Even though charging packs consistently make up 15-24% of all orders, they’ve never accounted for more than 3% of sales in terms of total dollar value.
- Apart from Airpods, computer hardware accounts for the majority of our revenue.

<b>Technical Analysis:</b><br>
In this section, I primarily used Tableau. SQL and BigQuery were also used to create a dataset for Tableau. My Tableau dashboard incorporates filters, tables, line graphs, and area charts.

You can find the SQL code for the dataset I created in BigQuery [here](https://github.com/sean-atkinson/elist_ecommerce_analysis/blob/main/sql/elist_dataset_tableau_query.sql).

Here is a peek of what the Tableau dashboard for this part of my analysis looks like:

<img width="750" alt="Tableau dashboard showing tables, line graphs, and area charts for total sales, total orders, and average time to ship" src="https://imgur.com/DpPG33J.png">

An interactive version of the above Tableau dashboard can be found [here](https://public.tableau.com/app/profile/sean.atkinson/viz/ElistOrdersDashboard_16896324404540/ordersdashboard).

A copy of my Tableau workbook can be found [here](https://github.com/sean-atkinson/elist_ecommerce_analysis/tree/main/tableau).

<a id='section_5'></a>
# Part 4: Recommendations & Next Steps
[(Back to table of contents)](#table_of_contents)<br><br>
- <b>Prioritize Expansion of the Loyalty Program:</b> Due to the current difficulty of marketing through channels outside of email, it's essential that this becomes a high priority. One retailer whose program we should look at is Altitude Sports. Altitude Sports typically employs a strategy of using very competitive pricing during high sales seasons like Black Friday to attract new potential customers. They then promote their [membership](https://www.altitude-sports.com/products/membership) to them by offering it for half price and doubling its discount for a limited time period. Additionally, throughout the year, they give members other benefits like member-only discounts and store credits to encourage them to spend money during non-peak seasons.
- <b>Focus on Broadening Our Reach into Revenue-Generating Product Categories:</b> Since computer hardware represents such an outsized portion of total sales in terms of dollars, consider exploring the possibility of adding additional computer hardware to our product assortment.
- <b>Integrate Key Financial Metrics into Analysis:</b> Incorporate customer acquisition costs and wholesale or costs of goods sold into analysis to get an understanding of customer lifetime value and what products perform best in terms of net profits. Insights from the latter point can guide us in identifying products that could help reverse our declining sales. 
- <b>Take a Closer Look at Shipping Fluctuations:</b> Investigate why shipping times are so volatile for iPhones and Bose headphones. Additionally, consider if the volatility, combined with poor sales numbers, means it's better to replace those products with something that might appeal more to our most valuable customer segments.

<a id='section_6'></a>
# Addendum: Notes on Data Cleaning
[(Back to table of contents)](#table_of_contents)<br><br>
Please note that as a part of the data cleaning stage, 15,200 entries were identified as duplicates in the initial Excel data. To maintain the integrity and reliability of my insights, these duplicates were removed from the final dataset used for my analysis. Therefore, the original list of entries, which initially consisted of 108,127 entries, was reduced to 92,927 after removing the identified duplicates. This decision was essential to ensure the validity of the observations made for this project.
