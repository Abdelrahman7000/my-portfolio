Hello there,

I am <b>Abdelrahman Shaban</b>.

I am a fresh graduate with a high academic record (ranked third). My major was in Management Information Systems. I have done many projects regarding ETL pipelines, Data Visualization, Web scraping using Beautifulsoup, and simple ELT using dbt (data built tool).

## Tools
one of the most interesting tasks in the data projects is to visualize your findings. For this, I use:

![tableabju](https://github.com/Abdelrahman7000/my-portfolio/assets/61333407/29db2d58-72df-49a1-91d4-db0d1b5a8bfd)

This is a sample of what I used to do:

![Screenshot from 2024-06-11 17-51-06](https://github.com/Abdelrahman7000/my-portfolio/assets/61333407/795dcebe-0d56-4ca3-b9a5-a887867dfea3)
I know what you're thinking, where can you find more interactive samples of my dashboards and charts?

<a href='https://public.tableau.com/app/profile/abdelrahman.shaban/vizzes'>Just Click Here.</a>

Also, SQL is my favorite tool to transform, analyze, and query the data. take a look at the following example for my SQL code:

        with cte as (
          SELECT ticker,max(open) highest_open
          from stock_prices
          GROUP BY 1
        ),
        
        cte2 as (
          SELECT ticker, min(open) lowest_open
          from stock_prices
          GROUP BY 1
        ),
        cte3 as (
          select cte.ticker,cte.highest_open,s.date highest_mth
          FROM cte 
          join stock_prices s
          on cte.highest_open=s .open
        ),
        
        cte4 as (
          select cte2.ticker,cte2.lowest_open,s.date lowest_mth
          FROM cte2 
          join stock_prices s
          on cte2.lowest_open=s.open
        )
        
        SELECT cte3.ticker,
                replace(to_char(cte3.highest_mth,'Mon-YYYY'),' ','') highest_mth,
                cte3.highest_open,
                replace(to_char(cte4.lowest_mth,'Mon-YYYY'),' ','') lowest_mth,
                cte4.lowest_open
        from cte3
        join cte4
        using (ticker)
        ORDER BY 1

I used SQL to do transformations on the data as part of an ELT process by:

![dbt](https://github.com/Abdelrahman7000/LeetCode/assets/61333407/8ea8cd6f-2473-4afb-8946-f9e4da3bbcf7)

I just started learning about dbt, and I began to do basic projects with it. This is an example of my code:

        {{
          config(
            materialized='view'
          )
        }}
        
        with cte as (
            select 
                c.CustomerID,
                c.CustomerName,
                c.Country,
                c.Email,
                c.Phone,
                n.NationName,
                n.Population,
                r.RegionName
            from {{ ref('stg_customers') }} c 
            inner join{{ ref('stg_nations') }} n on n.NationID=c.NationID
            inner join {{ ref('stg_regions') }} r on r.RegionID=n.RegionID
        )
        select *
        from cte

And here I wrote some tests and documentation:

        version: 2
        
        models:
          - name: stg_customers
            description: This model cleans the customer data, there is one record for each customer
            columns:
              - name: CustomerID
                description: Primary key
                tests:
                  - unique
                  - not_null
        
          - name: stg_orders
            description: This convert the data types of the order columns.
            columns:
              - name: OrderID
                tests:
                  - unique
                  - not_null
        
              - name: CustomerID
                tests:
                  - not_null
                  - relationships:
                      to: ref('stg_customers')
                      field: CustomerID
          
          - name: stg_nations
            columns:
              - name: NationID
                tests:
                  - unique
                  - not_null
            
          - name: stg_regions
            columns:
              - name: RegionName
                tests:
                  - accepted_values:
                      values: ['North America', 'Europe', 'Oceania', 'Asia', 'South America']
                    
          - name: customer_details
            description: This model joins regions, nations, and customers tables into one view. 
              

After doing our Transformations, and passing code reviews, I usually materialize the final model into:

![1_lAKDjzTTkKu9fbilA0LRLQ](https://github.com/Abdelrahman7000/LeetCode/assets/61333407/b6560ec2-4e39-4202-a163-0b32aca9dcd4)

For Orchestrating my ETL pipeline, I have basic skills in using:

![download (2)](https://github.com/Abdelrahman7000/LeetCode/assets/61333407/751e7da4-7810-4e5a-af93-1ad78bfe7499)


## My projects
<b>ETL for E-commerce data</b>
 * Designed and implemented data extraction processes from various sources into PostgreSQL staging tables for
data cleansing and transformation.
* Utilized Docker containers for creating isolated environments of PostgreSQL and Airflow.
* Orchestrated data workflows and scheduling tasks with Airflow, ensuring timely execution and monitoring of
ETL processes.
* Implemented transformations and business logic in Python using pandas to prepare data for loading into Big-
Query, aligning with the requirements of the star schema model.
* Loaded cleansed and transformed data into BigQuery data warehouse.
* Designed Tableau dashboards for visualizing my insights derived from the data.

<b>Time-Series-Employment-Analysis-of-NAICS</b>
 * Analyzed The North American Industry Classification System which is an industry classification system devel-
oped by the statistical agencies of Canada. The data covers the number of employees every month for many
sectors and industries.
 * Performed data preprocessing and data analysis techniques to extract insights from data.
 * Used EDA to answer questions related to the Business.

<b>Transforamation project using dbt and Google BigQuery</b>
 * In this project, I used the data build tool (dbt Cloud) with Google BigQuery to transform some data into an
aggregated format using some series of transformation models.

<b>Customer Churn Rate</b>
 * Creating a visual story on Tableau, which measures the churn rate of the customers.
