# # Chapter 2

# ## Using Classes: Instances

In order to access the properties and use the methods of a class, you first need to instantiate, or create an instance, of the class. When a class is instantiated, it returns an *individual object* of that class type that you can use. In PHP5, object instances are created using the **new** keyword, like so:

```
$c = new Circle();
```

Once an object is created, the individual properties and methods are accessed by using an “arrow” operator (a hyphen immediately followed by a greater-than sign), as shown in the following code:

```
```php
<?php


    class Circle
    {
        public $radius;

        public function calcArea($radius)
        {
            return pi() * pow($radius, 2);
        }
    }

    // Create a new instance of Circle
    $c = new Circle();

    // Change a property
    $c->radius = 5;

    // Use a method
    echo 'The area of the circle is ' . $c->calcArea(5);
?>
```
```

If you run the code, you will see something similar to:

```
The area of the circle is 78.539816339745
```

Looking at the code, you’ll see that you start out by defining the class Circle. Then, you added the code that instantiates the object:

```
// Create a new instance of Circle
$c = new Circle();
```

Finally, you changed the `$radius` property to a value of 5, and calculated the area of a circle given a radius of 5:

```
// Change a property
$c->radius = 5;

// Use a method
echo 'The area of the circle is ' . $c->calcArea($c->radius);
```