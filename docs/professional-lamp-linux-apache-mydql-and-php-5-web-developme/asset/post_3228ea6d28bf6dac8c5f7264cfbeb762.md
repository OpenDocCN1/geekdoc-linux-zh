
# Chapter 2

Running this code would produce the following:

```
The value of Pi in our Circle class is 3.14159265359
To recap, the value of Pi in our Circle class is 3.14159265359
```

In this example, you created the class constant Pi, which holds the value of, shockingly enough, the mathematical constant Pi. You then used a $self:: reference in the getPi() method to return the value of the class constant. It is important to notice the lack of a dollar sign in front of the name Pi when you access self::Pi. Class constants do not use the dollar sign prefix, where a standard class variable would.

> You are creating a Pi constant simply as an example. PHP already has a built-in pi() function that returns the value of Pi.

## Assignment versus Cloning

As you may already know by now, in standard PHP, there are two ways to assign data to a variable: assignment by value, and assignment by reference. The first, assignment by value, is most commonly used when setting simple values for variables, or copying other variables:

```
$a = 5;
$b = $a;
```

Here you are using assignment by value. When the value of $a is changed, $b remains unchanged; when you assigned $b = $a, you simply created a copy of the value of $a, and assigned that value to $b.

Assignment by reference is a bit different, however. Take the following example:

```
$a = 5;
$b =& $a;
```

In this example, you are assigning by reference, using the =& operator. When the value of $a is changed in this situation, $b would change as well — since $b was assigned, by reference, the value of $a, both variables point to the same location in memory, and when that value in memory is changed, both variables change as well.

In PHP5, all objects are assigned by reference, by default. This behavior is unlike PHP4, which assigned by value, unless the reference operator (&=) was used. In PHP5, if you want to make a copy of an object, instead of using a reference, you must use the clone statement, as follows:

```php
<?php

class Circle
{
    public $radius = 10;
}

// Create the original object and set its parameters
$original = new Circle();

// Create a cloned and assigned (by reference) object
$cloned = clone $original;
$assigned = $original;

// Now, change the original radius value:
$original->radius = 5;

// Show the state of all three objects
echo "\nOriginal:\n";
print_r($original);

echo "\nAssigned:\n";
print_r($assigned);

echo "\nCloned:\n";
print_r($cloned);
?>
```

This code will produce the following output:

```
Original:
Circle Object
(
        [radius] => 5
)

Assigned:
Circle Object
(
        [radius] => 5
)

Cloned:
Circle Object
(
        [radius] => 10
)
```

As you can see, `$assigned` references the `$original` object, but because you cloned `$cloned`, therefore making a detached copy of `$original`, its value doesn’t change when you modify `$original`.

# Inheritance and Interfaces

One of the benefits to using OOP with PHP5 is that it allows you to break down your code into logical chunks, in order to facilitate reuse. These chunks, when carefully written, can be reused again and again, in many different projects, leaving the programmer free to write code that is specific to the problem he or she is trying to solve.

In OOP, there are a couple of ways in which a group of methods and properties can be specified for use in multiple classes. The first, *inheritance*, allows you to define a base set of properties and methods that belong to a base class, and can be used as a building block for more specific classes. The second, *interfaces*, allow you to prescribe a list of methods that a class must implement.

## Inheritance

Suppose you are creating a code library, one for manipulation of different geometric shapes. The `Circle` class that you’ve been using throughout the chapter could be part of that very library. In creating different classes for different shapes — square, circle, triangle, and so on — you may find that you’re duplicating methods that are similar or identical among all shapes. This would be a good opportunity to use inheritance.

## The `extends` Keyword

Assume that all of the geometric shape classes are going to be drawn on a grid. Therefore, they will all need some sort of origin point $(x, y)$. You could include an origin property in each of the different classes, or using the `extends` keyword, you could use inheritance to define the property in one shared location. To do this, you’ll create a class named `Shape`, which will serve as a parent of all geometric classes that you might create. Each specific geometric shape class — be it a `Circle`, `Square`, `Ellipse`, or `Star` — all have a base set of functionality that `Shape` provides. An easy way to think of this parent-child relationship, is with the phrase “*is a*”. In this example, `Circle` *is a* `Shape`, just like a `Square` *is a* `Shape`, and a `Triangle` *is a* `Shape`.

To use your parent class `Shape`, you could do something similar to the following:

```php
<?php

class Shape
{
    public $origin = array('x'=>0, 'y'=>0);
}

class Circle extends Shape
{
    public $radius;
}

$c = new Circle();
print_r($c->origin);
?>
```

Running this code would produce the following:

```
Array
(
    [x] => 0
    [y] => 0
)
```

As you can see, you created a base class named `Shape` that defines a generic `origin` property. By using the `extends` keyword in the class definition for `Circle`, all properties and methods of `Shape` become part of the `Circle` object. Because `Circle` is a subclass of `Shape`, you can get the value of `$origin`, which is not defined explicitly in `Circle`—it’s inherited from `Shape`.

When extending base classes, it is possible to redefine the properties and methods that exist in the parent (base) class. For example:

```php
<?php

class Shape
{
    public $origin = array('x'=>0, 'y'=>0);  
}

class Circle extends Shape
{
    public $origin = 'New origin';
}

$c = new Circle();
print_r($c);
?>
```

This code would output the following:

```
Circle Object
{
   [origin] => New origin  
}
```

By redefining the base property `$origin` in the subclass, the new definition hides the parent’s values. Methods would behave the same way—redefining them in the subclass overrides the functionality of the parent method or methods. Take for example, the following code:

```php
<?php

class Shape
{
    public $origin = array('x'=>0, 'y'=>0);  
    public function getOrigin()
    {
        return $this->origin;  
    }
}

class Circle extends Shape
{
    public function getOrigin()
    {
        return array('x'=>1, 'y'=>1);  
    }
}

$c = new Circle();
print_r($c->getOrigin());
?>
```

In this example, the `getOrigin()` method defined in the `Shape` parent class is redefined in the `Circle` subclass. When calling `getOrigin()` on the instantiated `Circle` object, it returns `1,1` as the origin, and does not call the `getOrigin()` method in the base class `Shape`. A redefined method masks any same-named method in the parent class or classes.

## The final Keyword

In some situations, you want to prohibit a subclass from redefining a member that exists in a base class. You can prevent properties and methods from being redefined by using the `final` keyword:

```php
class Shape
{
    final public $origin = array('x'=>0, 'y'=>0);
}

class Circle extends Shape
{
    public $origin = 'This is invalid.';
}

$c = new Circle();
?>
```

If you attempt to run this code, a fatal error will occur:

```
Fatal error: Cannot declare property Shape::$origin final, the final modifier is  
allowed only for methods in /www/plamp/ch02/02-008.php on line 5
```

Since you used the `final` keyword in the base class's definition for `$origin`, when you tried to redefine it in the `Circle` subclass, it resulted in a fatal error.

Note that in the case of properties, the `final` keyword does not prohibit the changing of their values — only their redefinition.

## Using parent:: References

In some situations you may want to reference the original property or method from the base class, after you've redefined it in a subclass. To achieve this, you can use the `parent` keyword in conjunction with the `::` (double colon) you saw in the previous section on static members. For example:
