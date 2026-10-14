
However, even though the `include()` function failed, the rest of the PHP code continues processing. This may not be what you want to have happen.

## The require() Statement

The last example demonstrated another limitation of the `include()` statement. When it failed, it produced an error on the web page, but the PHP program just kept on going.

Sometimes you don't want to continue if an error occurs in your web page. Instead of just plowing through the rest of the code, you want the server to stop immediately so that the error message is the only thing you see. PHP has a solution for this.

The `require()` statement works exactly like the `include()` statement except for one difference: It forces the web server to stop all processing if it fails.

## Working with MySQL

The key to a dynamic web page is the ability to interact with the MySQL database to retrieve data to display on the web page. PHP provides a host of functions to interact with the MySQL server. Table 30-2 lists the main PHP functions you'll want to learn how to use.

| Function | Description |
|---|---|
| `mysql_connect(host, userid, password)` | Establish a connection with the MySQL server |
| `mysql_select_db(dbname, connection)` | Define a default database to interact with |
| `mysql_query(query)` | Submit an SQL statement to the MySQL server |
| `mysql_num_rows(result)` | Return the number of records present in a result set |
| `mysql_fetch_array(result, type)` | Retrieve the individual records from a query result set |

The basic flow of interacting with the MySQL server is:

- 1. Connect with the server.
- 2. Select a default database.
- 3. Submit an SQL query.
- 4. Retrieve the query result set one record at a time.

Here's an example of using the PHP MySQL functions to interact with a database and retrieve data:

```html
<html>
<body>
<h2>Product Listing</h2>
<?php
$connection = mysql_connect("localhost", "test", "test");
mysql_select_db("store", $connection);
$query = "SELECT prodid, description, price FROM products";
$result = mysql_query($query);
while ($row = mysql_fetch_array($result, MYSQL_ASSOC))
{
$prodid = $row['prodid'];
$description = $row['description'];
$price = $row['price'];

echo "$prodid - $description<br>\n";
echo "Cost: $$price<br><br>\n";
}
?>
</body>
</html>
```

This example submits a simple SELECT SQL statement to the MySQL server to retrieve three data fields from the products table.

## Object-Oriented PHP

One of the neat features about PHP is that as well as using standard procedural programming, it fully supports object-oriented programming (OOP). You can ease your way into the object-oriented world by applying the skills you've used in PHP.

In OOP, everything is related to a class. A class defines the characteristics of an object that you're using in your application. Every application revolves around handling objects. For example, a store application revolves around handling three objects: products, customers, and orders.

OOP classes define the objects that your application uses. Each class contains both the data and functions (called methods in OOP) required to interact with the object. Once you define the objects, all your application code needs to do is use the data and methods defined for the objects to process and manipulate them.

The benefit to OOP is that once you create a class for an object, you can use that same object any time in any other application, because you already have the code for using that object. Just plug in the class definition code, and you can use it in your application.

An OOP class consists of members. There are two types of members:

- Properties: Properties define attributes for the object (such as the description, price, and quantity in stock of a product). A class can contain many different property members, with each property describing a different feature of the object.
- Methods: A class method performs an operation using the properties defined in the class.

You create class methods to perform specific functions on the class data, such as a method to buy a product (where you subtract a value from the quantity property) or change the price of the product (where you add or subtract a value to the price property). Each class should be self-contained. The methods in a class should operate only on properties within the class and shouldn't deal with properties in other classes.
