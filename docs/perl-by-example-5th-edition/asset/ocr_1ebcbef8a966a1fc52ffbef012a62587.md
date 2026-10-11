+   e. Select the `ContactName`, `CompanyName`, and `Country` from the `Customers` table where the `Country` begins with either *Po* or *Sw*.

+   f. Find the total number of products in the `Products` table.

+   g. Print only the first 10 products from the `Products` table.

+   h. Select countries from the `Customers` table in alphabetic order with no duplicates.

+   i. Find all the products between $10 and $20.

+   j. Insert a new product.

+   k. Update the products table by adding $5.25 to the unit price of Sir Rodney’s Marmalade.

+   l. Select products below 10 units in stock.

+   m. Delete the oldest order in the database.

+   n. Use a SQL function to print the current date and time.

# Part 3—Perl/MySQL Lab

Consult the MySQL documentation (*mysql.com*) to get the correct datatypes and functions to help you with this lab. The documentation is excellent.

+   1. Create a SQL script called *school.sql* that will do the following:
+   a. `DROP DATABASE IF EXISTS SCHOOL;`
+   b. `CREATE SCHOOL;`
+   c. Create a table called *student*. It will consist of the following fields:
+   	*FirstName*
+   	*LastName*
+   	*Email*
+   	*CellPhone*
+   	*Major*
+   	*GPA*
+   	*StartDate*
+   	*StudentID* (primary key)

+   2. Use *school* and insert three rows of data into the *student* table.

+   3. At the MySQL prompt, execute the *school.sql* script. Use the SQL `describe` statement to see the structure of the *school* database.

+   4. Select all the rows in the *student* table. If the table has all the columns and data expected, then you are ready to go on to the next part of this lab.