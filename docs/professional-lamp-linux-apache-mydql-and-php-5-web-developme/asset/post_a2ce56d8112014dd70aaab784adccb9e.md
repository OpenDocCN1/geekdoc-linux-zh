
## Chapter 2

Finally, the `protected` keyword specifies that the property or method is available only within the defining class, and any other classes that extend or inherit from the defining class. Extending and inheriting classes are discussed later in the chapter.

> When reusing PHP4 classes under PHP5, it is important to keep in mind that properties defined with the var keyword, such as var $propertyName, will be treated as public, and an E_STRICT warning is issued.

Specifying the visibility for a class member is as easy as putting the appropriate prefix in front of the property or method declaration. In the Circle class that you defined earlier, all class members were defined as public. Now you're going to change some of the old class members to private, and add some new methods.

```php
<?php
class Circle
{
    private $center = array('x' => 0, 'y' => 0);
    private $radius = 1;

    public function setRadius($radius)
    {
        $this->radius = $radius;
    }
    public function setCenter($x, $y)
    {
        $this->center['x'] = $x;
        $this->center['y'] = $y;
    }
    public function calcArea()
    {
        return pi() * pow($this->radius, 2);
    }
}
?>
```

Instead of leaving the properties as public, you changed them to private and created functions to set their values. In simple situations such as this, it is probably overkill to do so, but if you were to expand the application, the set functions could be used to do complex calculations on data before setting the internal values. Such a separation can also add a layer of protection to the private members by validating the externally provided values before allowing the internal data to change.

You can use your modified class with the following code:

```php
<?php
$c = new Circle();
$c->setCenter(0,0);
$c->setRadius(10);

echo "The area of the circle is " . $c->calcArea() . "\n";

// Attempt to access a private property
echo "The private value of radius is " . $c->radius;
?>
```

If you run this code, you would see something like the following:

```
The area of the circle is 314.15926535898
Fatal error: Cannot access private property Circle::$radius in /www/plamp/ch02/02-002.php on line 31
```

As you can see, it is not much different from your previous use of Circle, but because of the public/private specifications, you must now use methods to access the $center and $radius properties, instead of accessing the properties directly. Notice what happens when you try to directly access a private member at the end- a fatal error occurs.

### Constructors and Destructors

In some situations when dealing with classes, you might want to have a way to automatically perform actions when the object is created. You might want to initialize object parameters or automatically call a class method. Perhaps you want the object to check the local environment to see that necessary resources are available or maybe even set up initial connections. For such situations, PHP provides constructors.

A constructor is nothing more than a specially named method that is automatically called when an object is instantiated. In PHP5, to implement a constructor, all you need to do is implement a method named __construct. For example:

```php
<?php
class Circle
{
 public function __construct()
 {
 // Perform actions when object is created
 echo "A circle object is being created.\n";
 }
}
$c = new Circle();
?>
```

When you execute this code, you see the following:

```
A circle object is being created.
```

As expected, the code defined inside the constructor method executed automatically when the object was instantiated.

> You can still use PHP4-style constructors (methods with the same name as the class) with PHP5, but the new-style __construct method is preferred.

Like standard methods and functions, constructors can also process arguments. To pass arguments to a constructor, you include them inside the parentheses when an object is created, like this:

```php
<?php

class Circle
{
    public $radius;

    public function __construct($r)
    {
        // Perform actions when object is created
        echo "A circle object is being created.\n";
        $this->radius = $r;
    }
}

$c = new Circle(10);
?>
```

In this example, you've simply provided a radius parameter when creating the object — 10 in this case — which is automatically interpreted by the constructor, which in turn sets the radius of the circle when instantiated.

Now that you have a way to perform actions when an object is created, you'll look at a way to perform additional actions when an object is destroyed. PHP5 now includes a special method that is called when an object is destroyed, referred to as, logically enough, a destructor. An object's destructor is called when all references to an object are removed, or it is manually destroyed in your code. Destructors are often used for various clean-up tasks, such as closing database connections and releasing file handles. To create a destructor, add a method to your class, and call it `__destruct`:

```php
<?php

class Circle
{
    public function __construct()
    {
        // Perform actions when object is created
        echo "A circle object is being created.\n";
    }

    public function __destruct()
    {
        // Perform actions when object is destroyed
        echo "A circle object is being destroyed.\n";
    }
}

$c = new Circle();

// Destroy the circle object
unset($c);
?>
```

Running this code gives you:

```
A circle object is being created.
A circle object is being destroyed.
```

Notice how you see the message placed inside the destructor, without having to do anything. This is because PHP automatically cleans up all references to objects when a script finishes executing, which automatically calls the destructors for objects.

One last thing to keep in mind is that unlike constructors, which can have parameters, destructors can have no parameters.

## Static Keyword

Sometimes when using object-oriented programming, you might need to access a method of a class, but without the need to create a full-blown object. To fill that need, PHP5 has provided the `static` keyword. New to PHP5, the `static` keyword allows class properties and methods to be available without instantiating the class. To make a class member static, just add the `static` keyword between the visibility and property or method definition, like so:

```php
<?php

class Circle
{
    public static function calcArea($r)
    {
        return pi() * pow($r, 2);
    }
}
?>
```

To use the newly created static property, you simply use the class name, followed by two colons, then the property name or method call:

```php
<?php
$r = 5;
echo "Given a radius of " . $r .
     ", a circle has the area " . Circle::calcArea($r);
?>
```

Running this code in your browser would produce results similar to the following:

```
Given a radius of 5, a circle has the area 78.539816339745
```

There are, however, some limitations to using static methods. Static methods cannot change or access object variables or methods using `$this->`; they can directly access only other static properties and methods in the class.

In order to access other static variables within the same class, you can use the `self` keyword, in conjunction with a double-colon. Using `self::` is similar to `$this->`, but it is for static members only. If you wanted to modify the `Circle` class to use static methods and properties, you might do something similar to the following:

```php
<?php
class Circle
{
    private static $radius;

    public static function setRadius($r)
    {
        self::$radius = $r;
    }

    public static function getRadius()
    {
        return self::$radius;
    }
}

Circle::setRadius(5);
echo "Our statically accessed circle has a radius of " .
       Circle::getRadius() . ".\n";
?>
```

A quick run through the PHP5 engine would produce the following:

> Our statically accessed circle has a radius of 5.

### Class Constants

Along with the improved object model in PHP5, the notion of class constants was introduced to PHP. Class constants are similar to regular PHP constants, but are available only within the definition of a class. Like standard PHP constants, their value can be set only once to a scalar value—a simple number or string—and any attempts to set a constant to the result of a function will result in an error.

When using class constants, keep in mind that they behave like static members in the way they are accessed—to access a class constant, you must use the double-colon (`::`) syntax. To define a class constant, use the `const` keyword before the constant name, as shown in the following code:

```php
<?php
class Circle
{
    const pi = 3.14159265359;

    public function getPi()
    {
        return self::pi;
    }
}

echo "The value of Pi in our Circle class is " . Circle::pi . "\n";
$c = new Circle();
?>
```
