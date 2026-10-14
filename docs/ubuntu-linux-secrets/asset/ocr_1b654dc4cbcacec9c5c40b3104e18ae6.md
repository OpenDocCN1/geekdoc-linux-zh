```
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

# Object-Oriented PHP

One of the neat features about PHP is that as well as using standard procedural programming, it fully supports object-oriented programming (OOP). You can ease your way into the object-oriented world by applying the skills you've used in PHP.

In OOP, everything is related to a class. A class defines the characteristics of an object that you're using in your application. Every application revolves around handling objects. For example, a store application revolves around handling three objects: products, customers, and orders.

OOP classes define the objects that your application uses. Each class contains both the data and functions (called methods in OOP) required to interact with the object. Once you define the objects, all your application code needs to do is use the data and methods defined for the objects to process and manipulate them.

The benefit to OOP is that once you create a class for an object, you can use that same object any time in any other application, because you already have the code for using that object. Just plug in the class definition code, and you can use it in your application.

An OOP class consists of members. There are two types of members:

+   Properties: Properties define attributes for the object (such as the description, price, and quantity in stock of a product). A class can contain many different property members, with each property describing a different feature of the object.
+   Methods: A class method performs an operation using the properties defined in the class.

You create class methods to perform specific functions on the class data, such as a method to buy a product (where you subtract a value from the quantity property) or change the price of the product (where you add or subtract a value to the price property). Each class should be self-contained. The methods in a class should operate only on properties within the class and shouldn't deal with properties in other classes.