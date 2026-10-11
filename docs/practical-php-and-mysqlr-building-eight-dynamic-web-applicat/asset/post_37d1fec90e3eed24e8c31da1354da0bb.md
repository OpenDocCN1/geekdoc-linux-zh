
very first field (the **id** field) stores this unique number. This unique field (be it a unique number or some other unique field such as a username) is called a **primary key**. You will use primary keys throughout the book.

The second field in the previous list is **cat_id**. This field is called a **foreign key** and will be matched to the primary key of the **categories** table, discussed next. The other fields in the table contain generic information about different aspects of the product.

The **categories** table contains a series of fields that pertain to the different types of product categories. This table includes the following fields:

- **id**
- **category**

As you can see, this table is rather simple, because the aim of the table is simply to provide a means to store information about the category. In this simple example, you will just store the name of the category in the table as well as its primary key field.

## How the Tables Relate to Each Other

With the two tables designed, it now makes sense to discuss how they relate to each other. The relationship that is created between the two tables is performed by matching certain types of information. In these two tables, this match is made between the **id** field in the **categories** table and the **cat_id** field in the **products** table. If both fields contain the same number, a relationship exists.

When you add records to the **products** table, instead of adding the text name of the category in the **cat_id** field, you instead store the **id** value associated with the relevant category. For example, if the first category in the **categories** table is *Swimming* and has an **id** of 1, you would store the number 1 in the **cat_id** field of the **products** table for a swimming-related product. Later, when you write code to pull information from the database, you can make use of these different relationships to pull different types of information.

At this point, you may be wondering what the benefits are of separating this information into separate tables. Why not just include the name of the category in the field? There are various practical reasons for this separation, as follows:

- The first benefit becomes obvious when you want to change the name of the **category**. If you wanted to broaden the category from *Swimming* to *Water Activities*, for example, you would need to go through each record and change the field manually. If you used two tables to separate the data, you would need to change only a single record to adjust the category, and then the changes would be reflected in all related records.
- If you use separate tables, you can associate more information with the category. There is no reason you could not add extra fields in the **categories** table later to add features such as a *description* of the category, *category icon*, *translated definitions*, and more.
- A big reason for extracting data into separate tables is ease of use. If you have a single table with a huge number of fields, it looks a lot more complex and difficult to deal with. It is better to have a number of simple, smaller tables.
- If you spread your data across a number of smaller tables, your database will perform more efficiently, because it will not need to trudge through endless amounts of irrelevant data.

Separating your information into different tables has a number of benefits, and it is certainly the *right* way to develop database-driven applications. You will see many examples of how this separation of data across tables works throughout the book.

## Creating the Database

The next step is to actually turn this theory into something you can see, touch, and work with. To do this, you need to make use of your database client. In this example, you will make use of phpMyAdmin, a tool included with **XAMPP**, to create the database.

First, open your Web browser and connect to **phpMyAdmin** by accessing http://localhost/phpmyadmin/. A login screen displays in response. If you have only just installed **MySQL**, or **XAMPP**, use the username *root* with no password. If you are working on a shared computer, change your *root* password by first connecting to the server with the following command:

```
mysql -u root mysql
```

Now *issue* the following SQL query:

```
SET PASSWORD FOR root@localhost=PASSWORD('chinnyraccoon');
```

Obviously, replace the password in the parentheses with your own password. After you have logged into phpMyAdmin, you will see a frame on the left side of the screen that is used to list databases and tables (nothing will be selected currently). In the main body of the screen is a box in which you can type a database name to be created (see Figure 2-2). In this box, type productssdb and click the Create button. You now see the productssdb database appear in the left frame. Ordinarily, your tables are listed under the database name on the side, but no tables have been created yet.

![](img/c75d0c4fa51711b62f211459ae794f3f_54_0.png)

**FIGURE 2-2** Creating a new database is simple in phpMyAdmin.

### Creating the Tables

In the main body of the screen is a box that you can use to create a table. In this box, type the name products and give it 5 fields. You will then be presented with the table design screen. As shown in Figure 2-3, there are five rows with a number of different boxes to configure each field in the table. The majority of these boxes will be irrelevant in this simple example.

Before you create the fields, it's necessary to discuss the concepts of types in MySQL. In any kind of database programming, the kind of information you store inside the database has different characteristics depending on what type of information it is. For example, if you store a float in a database (a float is a number with a decimal place, such as 21.45), more memory is required to store this type of information than storing an integer (a whole number, such as 35). In addition to this, different numbers of have different ranges. For example, the TINYINT type in MySQL can store any whole number between −128 and 127. As a contrast, the BIGINT data type can store anything from −9223372036854775808 to 9223372036854775807.

![](img/c75d0c4fa51711b62f211459ae794f3f_55_0.png)

**FIGURE 2-3** The table design screen has a lot of options; use the scroll bar to move along them.

In terms of memory usage and performance, there is the difference between storing a 1-byte value with TINYINT and storing an 8-byte value with BIGINT. Throughout this book, we will be using the major MySQL types extensively, and each example will explain why the relevant data type has been selected. This should give you a solid, practical idea of how different data types should be used.

Without further ado, it’s time now create the tables. In the first row of the Field column, add id as the name of the field. In the second column (Type), select the data type as MEDIUMINT; this will provide access for up to 8388607 products. Remember that this id column requires a unique value for each product, so you need to ensure that the data type is large enough to cater for the potential number of products you will need. Continue along the row, and then select the Extra box and select auto_increment from it. This option automatically fills the id field for you when you add a record. With this option enabled, each new record is given a value in the id column that is 1 larger than the id in the previous record. With auto_increment set, you can effectively ignore the id field and it will look after itself. The final option to set is the first radio button (it has an icon of a small key and a table). By selecting this option, you are making the field the primary key, and the database will not allow a duplicate value in this field. If you combine this option and auto_increment as done here, you can be assured that you will have a reliably unique primary key.
