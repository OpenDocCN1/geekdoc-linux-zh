
Now, go through each row in turn and add the following fields:

- **cat_id**: Add cat_id to the Field column and assign the type of TINYINT. Having more than 127 categories is unlikely, so this is a suitable type. You don't need to provide a length.
- **product**: Add product to the Field column and assign the type of VARCHAR. You can use this type when you need to store fewer than 255 letters in the field. You will need to supply a maximum length for the field when using the VARCHAR type. Add 50 as the length; it is unlikely a product title will be longer than 50 letters in size.
- **description**: Add description to the Field column and assign the type TEXT. You can use TEXT when you need to store potentially large chunks of text in a field. You don't need to supply a length.
- **price**: Add price to the Field column and assign the type FLOAT. You can use this type when you need to store numbers with a decimal place in them. You don't need to specify a length.

When you have configured your fields, click the Save button, and your table is created. One of the most useful benefits of using phpMyAdmin is that the SQL that is generated when you do something is always shown to you. This gives you a fantastic idea of how SQL works by just having a casual look at the generated code when you use phpMyAdmin. This SQL code will not make much sense right now, but have a look over it to get a gist of what SQL looks like. SQL is used extensively in the many projects later in the book, so it is advised you get used to reading through SQL as soon as possible.

The generated SQL should look fairly similar to this:

```sql
CREATE TABLE `products` (
  `id` MEDIUMINT NOT NULL AUTO_INCREMENT ,
  `cat_id` TINYINT NOT NULL ,
  `product` VARCHAR(50) NOT NULL ,
  `description` TEXT NOT NULL ,
  `price` FLOAT NOT NULL ,
  PRIMARY KEY ( `id` )
);
```

If you read the SQL from top to bottom, you will see how it is similar to English. Although you will rarely write SQL manually to create tables (you normally just create them in a client such as phpMyAdmin), the syntax to create a table is fairly straightforward.

Now you need to create the second table. To do this, click the perfectproducts link in the left frame. In the main body of the page, you can now create a new table called categories and give it 2 fields. In the table design screen, add the following fields:

- **id**: Add id to the Field column and assign the type TINYINT. Now select auto_increment from the Extra box and then select the Primary Key option in the column with the small key icon at the top.
- **category**: Add category to the Field column and assign the type VARCHAR. Set the length to 30.

When you have added these fields, click the Save button. You are finished.

### Adding Data to the Tables

With the tables complete, you are ready to load them with data. You will begin by doing this manually in phpMyAdmin, but as you work through the book, you will create forms to automate how the data is added to different tables.

First, you'll add some data to the *categories* table. You need to add some categories first so that you can reference the relevant categories in the *products* table. To add data, select the *categories* table from the tables list in the left frame. You should now see a number of tabs appear in the main body of the screen at the top. Click the Insert tab. You are taken to a screen in which you can add data into the table, as shown in Figure 2-4.

![](img/c75d0c4fa51711b62f211459ae794f3f_57_0.png)

**FIGURE 2-4** You can insert data two records at a time.

When adding information, you are given two sets of forms to add two records into the table at a time. You don’t need to use both, but it is handy to have two forms at the same time when entering test information, as you are doing here.

When you add the data, you don’t need to use any of the Function options. Also, remember to not add anything into the *id* field; *auto_increment* will deal with that for you. All you need to do is fill in a category in the Category field. Add the following categories one at a time:

- Swimming
- Soccer
- Baseball
- Cricket

When you have added these records, click the Browse tab in the main body of the page. You now see the table with the *id* values automatically filled in, as well as the categories that you added (see Figure 2-5).

![](img/c75d0c4fa51711b62f211459ae794f3f_58_0.png)

**FIGURE 2-5** Click the Browse tab to see the records inside a particular table.

Now, fill some data in the *products* table. To do this, click the *products* table in the left frame and then click the Insert tab again to add the following information into the form:

- In the first record, add 1 into the cat_id box (this puts this record in the Swimming category) and then add any swimming-related product that you can think of. (Be imaginative; it is always fun to add some kind of ludicrous product that gives you a chuckle when you deal with the record.) Add the price as a proper price (such as 21.99), but do not add the currency symbol.
- For the second record, add 3 to the cat_id box (this puts this record in the Baseball category). Again, add a fun product and add a normal price.

Feel free to add some more products, but remember to use the id from the categories table in the cat_id field. This will ensure you are relating the two tables properly.

# CONNECTING TO MYSQL IN PHP

With some core PHP experience and a database development behind you, now is the time to perform the all-important step of hooking the two together and connecting to the database in PHP. This involves you creating the database connection, then issuing a SQL query, and finally dealing with the results of the query in a way that makes sense in your Web application.

To actually connect to MySQL, PHP provides built-in support to make the connection, perform queries, and deal with the results. To do this, a number of PHP functions, prefixed with mysql_, make the magic happen. Although these functions are very useful, there may a case in the future when you want to be able to use any one of a number of databases with your Web application. With this requirement, you would need to use a third-party database abstraction library, such as PEAR::DB or ADO DB. If you know you will be using MySQL for a specific project, however, the mysql_ range of functions is perfectly suitable.

## Making the Connection

The first step is to actually make a connection to the database. This connection is used to communicate with the database when sending queries and data back and forth. To do this, you need to write some PHP that will pass the relevant authentication details to MySQL and, if you are authorized, give you a connection.

Create a new file called dbconnect.php and add the following code:

```php
<?php

$dbhost = "localhost";
$dbuser = "root";
$dbpassword = "";
$database = "productsdb";
$db = mysql_connect($dbhost, $dbuser, $dbpassword);
mysql_select_db($database, $db);
?>
```

The first four lines in the code create some variables that contain the relevant pieces of information that are required to connect to a database. It is important to remember that these four lines literally are just set a bunch of variables; no connection is made at this point. You can call these variables what you like, but you will need to provide legitimate information for the host, username, password, and database that you are using on the MySQL server.

After you set the variables, you can make the connection. This happens with the `$db = mysql_connect($dbhost, $dbuser, $dbpassword)` line. This line uses the mysql_connect() function to pass the host, username, and password variables to the MySQL server and put the result of the connection in the $db variable. You then use the $db variables as a pointer to the main connection. To keep the code simple, this example does not involve any error checking; often you would check to see if the connection is suitable and possibly display a suitable error message. Some programmers feel this is unnecessary as you will get a PHP error message anyway if the connection is rejected, but if you implement your own errors, you can format and reference your errors in a nicer way.

When the connection has been made, you need to select the database that you want to use (remember, MySQL can have a number of different databases). This is performed with the mysql_select_db() on the next line. Here you specify the variable with the chosen database and also specify the connection ($db) that the database should be selected from.

At this point, you are now connected. Any other MySQL-related connections on this page will be applied to the connection that has just been created.

![](img/c75d0c4fa51711b62f211459ae794f3f_60_0.png)

### Database Connections Are Per Page

The database connection you made does not span across other pages. You need to include the connection details on each page that needs to access MySQL. Of course, ways of making this more efficient will be covered later in the book.

At this point, you are ready to start playing with the database on this page.
