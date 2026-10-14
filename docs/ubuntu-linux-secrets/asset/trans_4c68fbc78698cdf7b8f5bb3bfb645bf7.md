
properties and modify them with whatever values it wants. That could be dangerous, and it's somewhat frowned upon in OOP classes. What if a wayward application set the price property of a product to a negative value? OOP allows you to code your classes to help prevent accidents like that.

The preferred way to handle properties in a class is to make them private so that any external code can't change them. It then creates public methods that allow programs to set and get the property values. You can control exactly what happens to the properties in those public methods. Let's create another example that demonstrates this technique:

- 1. Create a file called example2.php in the /var/www/html folder.
- 2. Open the file in a text editor and add the following code:

```
<?php
class Product {
    private $description;
    private $price;
    private $quantity;
    public function setDescription($value) {
        $this->description = $value;
    }

    public function getDescription() {
        return $this->description;
    }

    public function setPrice($value) {
        if ($value > 0)
            $this->price = $value;
        else
            $this->price = 0;
    }

    public function getPrice() {
        return $this->price;
    }

    public function setQuantity($amount) {
        $this->quantity = $amount;
    }

    public function getQuantity() {
        return $this->quantity;
    }

    public function printProduct() {
        echo "Product: $this->description<br>\n";
        printf("Price: $%.2f<br>\n", $this->price);
        echo "Quantity: $this->quantity<br>\n";
    }

    public function buyProduct($val) {
        $this->quantity -= $val;
    }
}
```

```
$prod1 = new Product();
$prod1->setDescription("Carrot");
$prod1->setPrice(1.50);
$prod1->setQuantity(10);
echo "Just added product:<br>\n";
$prod1->printProduct();
echo "<br>Buying 4 carrots...\n";
$prod1->buyProduct(4);
echo "Quantity is now: " . $prod1->getQuantity() . "<br>\n";
?>
```

- 3. Save the file and exit the text editor.
- 4. Open a browser and go to the URL http://localhost/example2.php.

You should see the same output as for the example1.php code. Notice that the new methods set the property values inside the class. Only those methods are allowed to access the properties directly. If you try using the code

```
$prod1->quantity = 10;
```

in your application, you'll get an error message, because the properties are now private. This safeguard provides a basic level of protection for your data. You can put any type of checks in the methods that set property values. The setPrice() method demonstrates this feature by checking the value that the program code assigns to the price property.

There's one downside to protecting your class properties, though: It's somewhat of a pain to create a new class object, because you have to use the individual set methods to define each property value. Fortunately, PHP provides an easy way to solve this problem.

## Class Constructors

Most OOP languages provide a special method called a constructor. The constructor allows you to automatically define property values when you instantiate an object. PHP uses the special method __construct() to define the constructor:

```
public function __construct($name, $value, $amount) {
$this->description = $name;
if ($value > 0)
$this->price = $value;
else
$this->price = 0;
$this->quantity = $amount;
}
```

The constructor for our Product class uses three parameters to assign values to the three class properties when you instantiate an object. To create a new Product object, you must use this format:

```
$prod1 = new Product("Carrot", 1.50, 10);
```

You can now use a constructor to force the program code to set the class properties when it instantiates the object. If you choose, you can also block any properties from changing by not providing methods that change the values. That's a lot of control over your code!

At the beginning of this section I mentioned that OOP programming allows you to use your classes in any application. The key is to create the class constructor as a separate program file. Try out this example:

- 1. For the Product class, create a file called Product.inc.php in the /var/www folder and add this code:

```
<?php
class Product {
private $description;
private $price;
private $quantity;

public function __construct($name, $value, $amount) {
$this->description = $name;
if ($value > 0)
$this->price = $value;
else
$this->price = 0;
$this->quantity = $amount;
}

public function setDescription($value) {
$this->description = $value;
}

public function getDescription() {
return $this->description;
}

public function setPrice($value) {
if ($value > 0)
$this->price = $value;
else
$this->price = 0;
}

public function getPrice() {
return $this->price;
}

public function setQuantity($amount) {
$this->quantity = $amount;
}
public function getQuantity() {
return $this->quantity;
}

public function printProduct() {
echo "Product: $this->description<br>\n";
printf("Price: $%.2f<br>\n", $this->price);
```
