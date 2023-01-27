# RelationalDatabases
IBM's Data Engineering Professinal Certificate Course 4

PostgreSQL, MySQL, DB2, pgAdmin, SQL.

In this scenario, I have recently been hired as a Data Engineer by a New York based coffee shop chain that is looking to expand nationally by opening a number of franchise locations. As part of their expansion process, they want to streamline operations and revamp their data infrastructure.

My job is to design their relational database systems for improved operational efficiencies and to make it easier for their executives to make data driven decisions.

Currently their data resides in several different systems: accounting software, suppliers’ databases, point of sales (POS) systems, and even spreadsheets. I will review the data in all of these systems and design a central database to house all of the data. I will then create the database objects and load them with source data. Finally, I will create subsets of data that your business partners require, export them, and then load them into staging databases that use different RDBMS.






Task 1 : Identifying entities.



![Task1](https://user-images.githubusercontent.com/114824225/215073960-8edc518f-4944-463c-b8f8-fc61d9e4f510.jpg)





Task 2 : Identitying attributes.




![Task2](https://user-images.githubusercontent.com/114824225/215073972-eed8532a-c05f-455b-bd5c-001a9e239fc9.jpg)





Task 3 : Creating an entity relationship diagram (ERD) using the pgAdmin ERD Tool.

3.1 First, I open a new terminal from the side-by-side Cloud IDE. I use the start_postgres command to start a PostgreSQL service session in the Cloud IDE.


![PostgreSQL from IDE](https://user-images.githubusercontent.com/114824225/215076849-ad983163-03c9-446f-8693-4e8bd4c0dde8.jpg)

3.2 I use the pgAdmin weblink to open pgAdmin in a new tab in my browser and then I create a new database named COFFEE, view the schemas in the new COFFEE database, and then start a new ERD project.


![COFFEE](https://user-images.githubusercontent.com/114824225/215077168-f72b42ea-06e3-4a33-9f68-dc399c843764.jpg)

3.3 I Add a table to the ERD for the sale transactions entity using the information provided by the bussiness. I consider what naming convention to use so that my colleagues will be able to understand my data and to ensure that the names are valid in other RDBMS. Then I use the sample data to determine appropriate data types for each column. I also add a table to the ERD for the product entity using the rest of the information provided. I also consider again what naming convention to use so that my colleagues will be able to understand my data and to ensure that the names are valid in other RDBMS. And use the sample data again to determine appropriate data types for each column.





![Task3A](https://user-images.githubusercontent.com/114824225/215074399-cabb4a7f-2a5f-4c3a-a2a9-7796f18de696.jpg)
![Task3B](https://user-images.githubusercontent.com/114824225/215074405-8ae635df-da71-497e-a2ab-850576bcd533.jpg)





Task 4 : Normalize tables.

When reviewing my ERD I notice that it does not conform to second normal form. I will normalize some of the tables within the database.

While reviewing the data in the sales transaction table I notice that the transaction id column does not contain unique values because some transactions include multiple products.

I then determine which columns should be stored in a separate table to remove the repeating rows and to put this table into second normal form.

After that, I add a new table named sales_detail to the ERD, defining the columns in the new table, and deleting the moved columns from the sales transaction table, leaving a matching column in each of two tables to later create a relationship between them.

Reviewing the data in the product table, I notice that the product category and product type columns contain redundant data. Therefore, I determine which columns should be stored in a separate table to reduce redundant data and to put this table into second normal form.

After that, I add a new table named product_type to the ERD, define the columns in the new table, and delete the moved columns from the product table, , leaving a matching column in each of two tables to later create a relationship between them.

![Task4A](https://user-images.githubusercontent.com/114824225/215074375-a116e39d-ec68-49ab-89bb-d6b6da6909c8.jpg)
![Task4B](https://user-images.githubusercontent.com/114824225/215074387-4d66bd60-ebaa-4328-8a6c-d1d700590907.jpg)





Task 5 : Define keys and relationships.

After normalizing the tables, I can define their primary keys and define relationships between the tables in my ERD, identifying an appropriate column in each table to be a primary key and creating the primary keys in the tables in your ERD.


I then identify the relationships between the following pairs of tables and then create the relationships in my ERD:

'sales_detail' to 'sales_transaction'
'sales_detail' to 'product'
'product' to 'product_type'

![Task5A](https://user-images.githubusercontent.com/114824225/215074351-352df903-df20-4458-ae01-f1086b4b9d49.jpg)
![Task5B](https://user-images.githubusercontent.com/114824225/215074363-81e1416c-4c4f-4eb5-a9ad-40a034c9a047.jpg)





Task 6 : Create database objects by generating and running the SQL script from the ERD Tool.

Now that my design is complete, I will generate an SQL script from my ERD which I could use to create your database schema. For the purposes of this project, I will then use a provided SQL script to ensure that I will be able to successfully load the sample data into the schema. Finally, I will load the existing data from the various data sources into my new database schema.

Using the Generate SQL functionality in the ERD Tool, I create an SQL script from your ERD.

Then, I download the GeneratedScript.sql file to my local computer storage ('GeneratedScript.sql'). In pgAdmin, I open the Query Tool, uploading and openning the GeneratedScript.sql file from my local computer storage, and then I execute the script to create the tables defined in the ERD, verifying that the tables now exist in the public schema of the COFFEE database.

Next, I download the CoffeeData.sql file to my local computer storage ('CoffeeData.sql'). In pgAdmin, I open another instance of the Query Tool, uploading and openning the CoffeeData.sql file from my local computer storage, and then I execute the script to populate the tables you just created.

In pgAdmin, I review the first 100 rows of the sales_detail table.



![Task6A](https://user-images.githubusercontent.com/114824225/215074313-cbb3feb5-b281-40d9-b7a4-26c36b5d6eae.jpg)
![Task6B](https://user-images.githubusercontent.com/114824225/215074312-29dbb477-53d1-4045-99e1-4fe03e1db756.jpg)




Task 7 : Create a view and export the data.

The external payroll company have requested a list of employees and the locations at which they work. This should not include the CEO or CFO who own the company. In this task, I will create a view in my PostgreSQL database that returns this information and export the results to a CSV file.

In my COFFEE database, I create a new view named staff_locations_view using the following SQL:

1 SELECT staff.staff_id,


2 staff.first_name,


3 staff.last_name,


4 staff.location


5 FROM staff


6 WHERE "position" NOT IN ('CEO', 'CFO');


I view all the rows returned from the view to make sure the process went smoothly and then I save the results of the query to a file named staff_locations_view.csv on my local computer storage.


![Task7](https://user-images.githubusercontent.com/114824225/215074296-613542f9-7dde-4abe-8b06-c531175e4c6e.jpg)


Task 8 : Create a materialized view and export the data.
In my COFFEE database, I create a new materialized view named product_info_m-view using the following SQL:

1 SELECT product.product_name, product.description, product_type.product_category


2 FROM product


3 JOIN product_type


4 ON product.product_type_id = product_type.product_type_id;



I refresh the materialized view with data so it displays the up-to-date data and i view all the rows returned from the view. Then, I save the results of the query to a file named product_info_m-view.csv on my local computer storage.


![Task8](https://user-images.githubusercontent.com/114824225/215074290-fd8fd5ef-f68a-4803-a803-213fb5f55e50.jpg)





Task 9 : Import data into Datasette.
The external payroll company have asked me to upload the staff location information to their Datasette database.

I copy and enter this URL: https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0110EN-SkillsNetwork/Datasetteoptionallabs/Week4/data/staff_locations_view.csv of the staff_locations_view.csv file, which contains the staff location information and i explore the new table and then view the data in it.



![Task9](https://user-images.githubusercontent.com/114824225/215074282-74a5965b-7b0e-4584-a35e-112976c1f728.jpg)





Task 10 : Import data into a MySQL database.

The marketing consultant has asked me to upload the product information to their MySQL database. In the terminal from the side-by-side Cloud IDE, I use the start_mysql command to start a My SQL service session in the Cloud IDE. I use the browser weblink to open phpMyAdmin in a new tab in my browser.

In phpMyAdmin, I create a new database named coffee_shop_products, and then I import the product information saved in the product_info_m-view.csv file from my materialized view into a new table in the coffee_shop_products database. Finally, I briefly browse the contents of the new table to make sure the process was succesful.


![Task10](https://user-images.githubusercontent.com/114824225/215074273-c9314429-d299-4de3-a70f-44ce34af0939.jpg)


