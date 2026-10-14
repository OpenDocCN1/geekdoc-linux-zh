properties and modify them with whatever values it wants. That could be dangerous, and it's somewhat frowned upon in OOP classes. What if a wayward application set the price property of a product to a negative value? OOP allows you to code your classes to help prevent accidents like that.

The preferred way to handle properties in a class is to make them private so that any external code can't change them. It then creates public methods that allow programs to set and get the property values. You can control exactly what happens to the properties in those public methods. Let's create another example that demonstrates this technique:

+   1. Create a file called example2.php in the /var/www/html folder.

+   2. Open the file in a text editor and add the following code:

```
<\?php
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
```