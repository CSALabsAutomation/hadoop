 ### Data Ingestion into Hive Tables
 
 1. Initiate hive
 
    ```
    hive
    ```
 
 2. Create a database retail_org

    ```
    create database retail_org;
    ```
 
 3. Initiate a spark shell with postgresql jar file.
   
     ```
     spark/spark-3.3.1-bin-hadoop3/bin/pyspark --jars /home/hdoopuser/postgresql-42.5.1.jar
     ```


 2. Creating the dataframe for 3 tables.

    ```
        Sales_orders_df=spark.read.format("jdbc").option("url","jdbc:postgresql://127.0.0.1:5432/retail_org").option("driver","org.postgresql.Driver").option("Database","retail_org").option("dbtable","sales_orders").option("user","postgres").option("password","postgrespw").load()  
    ```
 
    ```
    customers_df=spark.read.format("jdbc").option("url","jdbc:postgresql://127.0.0.1:5432/retail_org").option("driver","org.postgresql.Driver").option("Database","retail_org").option("dbtable","customers").option("user","postgres").option("password","postgrespw").load()
    ```
  
    ```
    products_df=spark.read.format("jdbc").option("url","jdbc:postgresql://127.0.0.1:5432/retail_org").option("driver","org.postgresql.Driver").option("Database","retail_org").option("dbtable","products").option("user","postgres").option("password","postgrespw").load()
    ```
 
 3. Write the dataframes into hive table.

    ```
    Sales_orders_df.write.mode("Overwrite").option("path", "hdfs://localhost:9000/user/hive/warehouse/sales_orders").saveAsTable("retail_org.sales_orders")
    ```
    
    ```
    customers_df.write.mode("Overwrite").option("path", "hdfs://localhost:9000/user/hive/warehouse/customers").saveAsTable("retail_org.customers")
    ```
    
    ```
    products_df.write.mode("Overwrite").option("path", "hdfs://localhost:9000/user/hive/warehouse/products").saveAsTable("retail_org.products")
    ```
 
    
 
5. Import the packages 

    ```
    from pyspark.sql.types import * 
    ```

6. Create product structtype 

     
     ```
     ps_schema = StructType([StructField("product_id", StringType(), False),StructField("product_category", StringType(), False),StructField("product_name", StringType(), False),StructField("sales_price",StringType(),False),StructField("ean13", DoubleType(), False),StructField("ean5", StringType(), False),StructField("product_unit", StringType(), False),StructField("product_identity", StringType(), False)])
     
     ```
     
7. Convert the dataframe into list object for reassigning the structtype.

   ```
   data= product_df.rdd.map(lambda x: x)
   ```
 
8. Creating new dataframe with structtype.
 
   ``` 
   product_df = spark.createDataFrame(data=data,schema=ps_schema)
   ```

9. Save the dataframe into Hive table.

   ```
   product_df.write.mode("Overwrite").option("path", "hdfs://localhost:9000/user/hive/warehouse/products").saveAsTable("retail_org.products_raw")
   ```
