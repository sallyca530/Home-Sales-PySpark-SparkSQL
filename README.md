# Home-Sales-PySpark-SparkSQL


A Spark DataFrame is created from the dataset. (5 points)

![](images/Opt_3.png)


A temporary table of the original DataFrame is created.  

    home_sales_df.createOrReplaceTempView('home_sales')

A query is written that returns the average price, rounded to two decimal places, for a four-bedroom house that was sold in each year. 

    spark.sql("""
            SELECT YEAR(date),
            Round(AVG(price),2)
            AS AveragePrice
            FROM home_sales
            WHERE bedrooms==4
            GROUP BY YEAR(date)
            ORDER BY Year(date) ASC
            """).show()

![](images/Opt_3.png)

A query is written that returns the average price, rounded to two decimal places, of a home that has three bedrooms and three bathrooms for each year the home was built. 

    spark.sql("""
            SELECT YEAR(date_built) AS date_built,
            Round(AVG(price),2) AS AveragePrice
            FROM home_sales
            WHERE bedrooms==3 
            And bathrooms==3
            GROUP BY YEAR(date_built)
            ORDER BY date_built ASC
            """).show()

A query is written that returns the average price of a home with three bedrooms, three bathrooms, two floors, and is greater than or equal to 2,000 square feet for each year the home was built rounded to two decimal places. 

    spark.sql("""
            SELECT YEAR(date_built) AS date_built,
            Round(AVG(price),2) AS AveragePrice
            FROM home_sales
            WHERE bedrooms==3 
            And bathrooms==3
            And floors==2
            And sqft_living>=2000
            GROUP BY YEAR(date_built)
            ORDER BY date_built ASC""").show()

A query is written that returns the average price of a home per "view" rating having an average home price greater than or equal to $350,000, rounded to two decimal places. (The output shows the run time for this query.) (10 points)

A cache of the temporary "home_sales" table is created and validated. (10 points)

The query from step 6 is run on the cached temporary table, and the run time is computed. (10 points)

A partition of the home sales dataset by the "date_built" field is created, and the formatted parquet data is read. (10 points)

A temporary table of the parquet data is created. (10 points)

The query from step 6 is run on the parquet temporary table, and the run time is computed. (10 points)

The "home_sales" temporary table is uncached and verified. (10 points)