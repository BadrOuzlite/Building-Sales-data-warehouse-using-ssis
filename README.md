# Creating a Dynamic Sales Data Warehouse with SSIS

## Preview:
Using the [AdventureWorks2017](https://learn.microsoft.com/en-us/sql/samples/adventureworks-install-configure?view=sql-server-ver16&tabs=ssms) dataset, I’ve developed a Sales Data Mart with SQL Server Integration Services (SSIS). This project harnesses the power of SSIS and SQL Server modeling, delivering a Data Mart that enhances data management and analytics capabilities within organizations. Its numerous benefits make it an essential asset for effective data-driven decision-making.

## Tools and Technologies:
* Visual Studio
* SQL Server Integration Services (SSIS)
* SQL Server Management Studio (SSMS)
* Slowly Changing Dimensions (SCD) - Type 1 and Type 2
* Power BI (IN progress)

  
### Note:
This data mart is designed for online sales only.

## Project Phases

**1- Data Source Selection:**

* We began by selecting the AdventureWorks2017 database as our primary data source. This OLTP system serves as the foundation for our data warehouse.

**2- Data Extraction:** 

* Using SQL Server Integration Services (SSIS), we extracted relevant data from the AdventureWorks2017 database. This extraction process involved identifying essential tables and fields for analysis.

**3- Data Cleansing and Preprocessing:**

* To ensure data quality and accuracy, we performed data cleansing and preprocessing tasks. This step involved handling missing values, removing duplicates, and transforming data as needed.

**4- Star Schema Design:**

* The foundation of our data warehouse is the star schema. We meticulously designed this schema to align with the specific analytical requirements of our project. This schema includes dimension tables describing various attributes and a central fact table containing numerical measures.

**5- ETL Development:**

* The core of our data integration process is the development of Extract, Transform, Load (ETL) processes. Leveraging SSIS, we created workflows to extract data, apply transformations, and load it into the star schema.

**6- Data Warehouse Population:**

* We populated the data warehouse with cleansed and transformed data, ensuring that it is readily available for analysis.

- These phases represent the key milestones in our journey to create a Sales Data Warehouse using SSIS and SQL Server. The resulting star schema empowers my mindset with an efficient view of data access and valuable insights for informed decision-making.


### Star Schema Design:
I meticulously designed a star schema that serves as the foundation of our data warehouse. This schema features four dimension tables—Product, Customer, Territory, and Date—along with a central fact table that contains our key measures and surrogate keys from the dimension tables. This design ensures a robust framework for efficient data analysis and reporting, making our data warehouse well-structured and optimized for our specific analytical requirements.

* I’ve also generated some SQL scripts that can assist you in creating the schema structure for the sales data warehouse: [Scripts](https://github.com/BadrOuzlite/Building-Sales-data-warehouse-using-ssis/tree/main/Table%20Creation) 

![Sales Data Mart Star Schema](https://github.com/BadrOuzlite/Building-Sales-data-warehouse-using-ssis/blob/main/Images/sales_data_warehouse_schama.png)


### SSIS Packages:
I have created seven packages to build this data mart 
* ETL_Dim_Product
* ETL_Dim_Customer
* ETL_Dim_Territory
* ETL_Dim_Date
* Fact_Sales_Full_Load
* Fact_Sales_Increamental_Load
* Main (The entire ETL process)
  
![SSIS Packages](https://github.com/BadrOuzlite/Building-Sales-data-warehouse-using-ssis/blob/main/Images/SSISPackages.png)

### Product Dimension First Load:
This is the initial load for the Product dimension. As you can see, I utilized Slowly Changing Dimensions (SCD) Type 1 and Type 2. Since this is the first load, all records have been inserted into the destination database without going through any of the historization processes.

![Product Dim First Load](https://github.com/BadrOuzlite/Building-Sales-data-warehouse-using-ssis/blob/main/Images/Product_dim_firs_load.png)

### Product Dimension After Changes:

* After the initial load of our Product dimension, we focused on refining and enhancing this essential component. During this phase, we applied Slowly Changing Dimensions (SCD) techniques, specifically Type 1 and Type 2, to manage updates to the dimension data.
* **Result:** As shown in the accompanying image, this stage represents the Product dimension after the necessary updates were implemented. It highlights our commitment to data accuracy and our capability to effectively capture changes. The revised dimension now aligns with our evolving business needs, ensuring that our data mart continues to deliver valuable insights for informed decision-making.
* The changes apply to the database in this [SQL SCRIPT](https://github.com/BadrOuzlite/Building-Sales-data-warehouse-using-ssis/blob/main/Table%20Creation/Operation_check_on_dim_product.sql)


![Product Dimension After Changes](https://github.com/BadrOuzlite/Building-Sales-data-warehouse-using-ssis/blob/main/Images/Product_dim_second_load.png)

### Customer Dimension First Load:

* The Customer dimension is a crucial part of our data mart, and its initial load represents a significant milestone in our project. In this phase, we executed the first load of data into the Customer dimension, filling it with essential customer information.

* As shown in the accompanying image, the data smoothly transitioned through the ETL (Extract, Transform, Load) processes, leading to the successful insertion of customer records into the destination database. It’s important to highlight that this is the first load, during which all records are inserted without going through any historicization or change-tracking processes associated with SCD Type 1 and Type 2.

  
![Customer Dim First Load](https://github.com/BadrOuzlite/Building-Sales-data-warehouse-using-ssis/blob/main/Images/Customer_dim_First_load.png)

### Customer Dim After Making Changes:

* Building on the foundation of our Customer dimension, we initiated a phase dedicated to refining and enhancing this critical dimension. Following the initial load, we implemented adjustments and updates using data management techniques.
* As showcased in the accompanying image, this stage portrays the Customer dimension after incorporating modifications. These enhancements may include updates to customer information, the application of Slowly Changing Dimensions (SCD) techniques, and the adoption of change-tracking mechanisms. These efforts are aimed at ensuring that our Customer dimension accurately represents the evolving landscape of our customer data.

![Customer Dim After Making Changes](https://github.com/3amory99/Building-Sales-Data-Mart-Using-ETL-SSIS/blob/master/Output%20Images/Customer%20Dim%20After%20Making%20Changes.PNG)

### Territory Dim Load:

We find that the [CountryRegionCode] in [AdventureWorks2022] database is considered to only two letters like "US", "CA", "FR" So I have created a table called dbo.lookup_country with the total name of the country like "United States" to be able to ingest data into the data mart.

![Territory Dim](https://github.com/3amory99/Building-Sales-Data-Mart-Using-ETL-SSIS/blob/master/Output%20Images/Territory%20Dim.PNG)

### Date Dim Load:

Extract the date data from the Excel Sheet, you can find it here [Scripts](https://github.com/3amory99/Building-Sales-Data-Mart-Using-ETL-SSIS/tree/master/Scripts) 

![Date Dim](https://github.com/3amory99/Building-Sales-Data-Mart-Using-ETL-SSIS/blob/master/Output%20Images/Date%20Dim.PNG)

### Fact Table Full Load:

![Fact Table Full Load Control Flow](https://github.com/3amory99/Building-Sales-Data-Mart-Using-ETL-SSIS/blob/master/Output%20Images/Fact%20Table%20Full%20Load%20Control%20Flow.PNG)

![Fact Table Full Load Data Flow](https://github.com/3amory99/Building-Sales-Data-Mart-Using-ETL-SSIS/blob/master/Output%20Images/Fact%20Table%20Full%20Load%20Data%20Flow.PNG)

### Fact Table Incremental Load:

![Fact Table Incremental Load Control Flow](https://github.com/3amory99/Building-Sales-Data-Mart-Using-ETL-SSIS/blob/master/Output%20Images/Fact%20Table%20Increamental%20Load%20Control%20flow.PNG)

![Fact Table Full Load Data Flow](https://github.com/3amory99/Building-Sales-Data-Mart-Using-ETL-SSIS/blob/master/Output%20Images/Fact%20Table%20Full%20Load%20Data%20Flow.PNG)

### Insert New 5 Records in Sources:

![Insert New 5 Records in Sources](https://github.com/3amory99/Building-Sales-Data-Mart-Using-ETL-SSIS/blob/master/Output%20Images/Insert%20New%205%20Records%20in%20Sources.PNG)

### Fact Table Incremental Load:

![Increamental Load Data flow](https://github.com/3amory99/Building-Sales-Data-Mart-Using-ETL-SSIS/blob/master/Output%20Images/Increamental%20Load%20Data%20flow.PNG)

### Check the new insertion data in the Fact Table :

![Increamental data Result](https://github.com/3amory99/Building-Sales-Data-Mart-Using-ETL-SSIS/blob/master/Output%20Images/Increamental%20Result.PNG)

