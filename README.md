Hello there,

I am <b>Abdelrahman Shaban</b>.

I am junior data engineer with a high academic record (ranked third). My major was Management Information Systems.
As part of my learning journey, I got the following certificates:

<img width="200" alt="DE Associate - Facebook - Post" src="https://github.com/user-attachments/assets/27bd6999-2f0d-4374-8fbc-e6ab8f0247cc">
<img width="200" alt="DE Associate - Facebook - Post" src="https://github.com/Abdelrahman7000/my-portfolio/assets/61333407/8a24406c-efe9-495a-b522-ac89ce44026b">
<img width="200" alt="DE Associate - Facebook - Post" src="https://github.com/user-attachments/assets/57797d95-4fa5-4b69-81c0-0c49d2d42c1a">
<img width="200" alt='DE Associate - Facebook - Post' src="https://github.com/user-attachments/assets/551c3e7e-ae61-44df-be6a-7d4b1e8521ce">


 I have done many projects regarding ETL pipelines, Data Visualization, Web scraping using Beautifulsoup, and simple ELT pipelines using dbt (data built tool).

## Tools
* In the early stages of any data pipeline (e.g. ETL and ELT), I leverage Python scripts for extracting and transforming data from diverse sources. To streamline and enhance the extraction process, Additionally, I employ Airbyte to streamline the extraction process:

<img width="500" alt="Airbyte" src="https://github.com/user-attachments/assets/aeabb0ce-ca2c-4b05-84f2-2c08751d9254">

* Also, I use Alteryx for data preparation, transformation, analysis. This was a part of a project that I used alteryx as part of it:
<img width="900" alt="DE Associate - Facebook - Post" src="https://github.com/user-attachments/assets/9b7aa7db-4ab1-41c1-9fb8-c2afb81bd3e8">

* Also, SQL is my favorite tool to transform, analyze, and query data. take a look at the following example for my SQL code:

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

<img width="500" alt="DBT" src="https://github.com/Abdelrahman7000/LeetCode/assets/61333407/8ea8cd6f-2473-4afb-8946-f9e4da3bbcf7">

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
              

* After doing our Transformations, and passing code reviews, I usually materialize the final model into:

<img width="500" alt="Google BigQuery" src="https://github.com/user-attachments/assets/6b54d820-2515-4f38-abc2-cb78761fa2f6">


* For Orchestrating my ETL pipeline, I have basic skills in using:

<img width="500" alt="Google BigQuery" src="https://github.com/Abdelrahman7000/LeetCode/assets/61333407/751e7da4-7810-4e5a-af93-1ad78bfe7499">




* One of the most interesting tasks in the data projects is to visualize your findings. For this, I use:

<img width="500" alt="Google BigQuery" src="https://github.com/Abdelrahman7000/my-portfolio/assets/61333407/29db2d58-72df-49a1-91d4-db0d1b5a8bfd">


This is a sample of what I used to do:

![viz](https://github.com/Abdelrahman7000/my-portfolio/assets/61333407/9d5678bf-877a-445c-a5fe-8fb5dd3be1f3)


![Screenshot from 2024-06-11 17-51-06](https://github.com/Abdelrahman7000/my-portfolio/assets/61333407/795dcebe-0d56-4ca3-b9a5-a887867dfea3)
I know what you're thinking, where can you find more interactive samples of my dashboards and charts?

<a href='https://public.tableau.com/app/profile/abdelrahman.shaban/vizzes'>Just Click Here.</a>


## My projects
<b>Sales analytics using dbt</b> <a href='https://github.com/Abdelrahman7000/sales-analytics'>🔗</a>
 * Extracted the data from SQL Server and loaded it into PostgreSQL using Airbyte.
 * Scheduled the extraction process with Cron.
 * Used EDA to answer questions related to the Business.
 * Utilized Docker containers to create isolated environments of PostgreSQL and Airbyte.
 * Transformed the loaded data using DBT and built a star schema model.
 * Visualized the final results with Tableau.

<b>ETL for E-commerce data</b> <a href='https://github.com/Abdelrahman7000/bigquery-etl-pipeline'>🔗</a>
 * Designed and implemented data extraction processes from various sources into PostgreSQL staging tables for
data cleansing and transformation.
* Utilized Docker containers to create isolated environments of PostgreSQL and Airflow.
* Orchestrated data workflows and scheduling tasks with Airflow, ensuring timely execution and monitoring of
ETL processes.
* Implemented transformations and business logic in Python using pandas to prepare data for loading into Big-
Query, aligning with the requirements of the star schema model.
* Loaded cleansed and transformed data into BigQuery data warehouse.
* Designed Tableau dashboards for visualizing my insights derived from the data.

<b>Time-Series-Employment-Analysis-of-NAICS</b> <a href='https://github.com/Abdelrahman7000/DataInsight_Assignment_Time-Series-Employment-Analysis-of-NAICS'>🔗</a>
 * Analyzed The North American Industry Classification System which is an industry classification system devel-
oped by the statistical agencies of Canada. The data covers the number of employees every month for many
sectors and industries.
 * Performed data preprocessing and data analysis techniques to extract insights from data.
 * Used EDA to answer questions related to the Business.

<b>Transforamation project using dbt and Google BigQuery</b>  <a href='https://github.com/Abdelrahman7000/dbt_intro'>🔗</a>
 * In this project, I used the data build tool (dbt Cloud) with Google BigQuery to transform some data into an
aggregated format using some series of transformation models.

<b>Customer Churn Rate</b>
 * Creating a visual story on Tableau, which measures the churn rate of the customers.
