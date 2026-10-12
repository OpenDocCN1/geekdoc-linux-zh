
## Chapter 2

### __call

The magic method `__call` allows you to provide actions or return values when undefined methods are called on an object. The `__call` magic method can be used to simulate method overloading, or even to provide smooth error handling when an undefined method is called on an object. `__call` takes two arguments: the name of the method and an array of the arguments passed to the undefined method. For example:

```php
<?php

class Circle
{
    public function __call($m, $a)
    {
        echo "The method " . $m . " was called.\n".
             "The arguments were as follows:\n";
        print_r($a);
    }
}

$c = new Circle();
$c->undefinedmethod(1, 'a', 2, 'b');
?>
```

When you run this code, you would see something similar to the following:

```
The method undefinedmethod was called.
The arguments were as follows:
Array
(
    [0] => 1
    [1] => a
    [2] => 2
    [3] => b
)
```

Here you’ve defined a `__call` function to handle the call to the `undefinedmethod` method. As expected, it took the comma-delimited list of arguments and turned them into an array, which were captured in the `$a` parameter.

### __get and __set

The magic methods `__get` and `__set` allow you to specify custom functions to store and retrieve data in properties that aren’t already defined in the class.

`__get` takes one argument, the name of the property, while `__set` requires two: the name of the property and the new value.

```php
<?php
class Circle
{
    public function __get($p)
    {
        return $this->$p;
    }

    public function __set($p, $v)
    {
        $this->$p = $v;
    }
}

$c = new Circle();
$c->nonexistant = 5;
echo "The value of our nonexistant property: " . $c->nonexistant;
?>
```

When you execute the preceding code, PHP recognizes immediately that no property named 'nonexistant' exists in the class. Since the named property doesn't exist, the `__set()` method is called, which then assigns the value to the newly-created property of the class, allowing you to see the following:

```
The value of our nonexistant property: 5
```

In this example, you created the magic methods `__get` and `__set` to handle any undefined property accesses, and proceeded to use an undefined property named `nonexistant`.

### __sleep

When you use PHP classes to store data that must persist across pages or long periods of time, you can store the object using your favorite method of persistence (files, database, session variables, or cookies), but the objects must first be prepared.

When you're rereading object data to be stored, use the `serialize()` function. The `serialize()` function takes any complex data structure and converts it into a string that can be stored using your method of choice. Conversely, to retrieve your persisted data, use the `unserialize()` function. The `unserialize()` function takes your serialized string and converts it back to whatever complex structure it used to be.

To give the developer more flexibility when dealing with the serialization of objects, the `__sleep` and `__wakeup` magic methods are provided.

The `__sleep` magic method, if defined in the class, is automatically called immediately before the object is serialized. This method is extremely useful for closing database connections and cleaning up object resources.

The `__sleep` method can also return an array containing the names or object values to be serialized, which is useful when dealing with large objects. Only the necessary data will be serialized while other data can be ignored.

### __wakeup

The `__wakeup` magic method does the exact opposite of the `__sleep` method. When `unserialize()` is called, `__wakeup` is automatically called, which is helpful for resetting object values, restoring connections, and other initialization tasks.

Look at this simple example of `__sleep` and `__wakeup` in action. This example is going to require two files. The first file, you’ll create as page1.php:

```php
<?php
session_start();

class Circle
{
    public $radius;

    public $origin = array('x'=>0, 'y'=>0);
    public function __sleep()
    {
        echo 'zzzzz';

        return array('radius','origin');
    }

    public function __wakeup()
    {
        echo 'good morning!';
    }
}

$c = new Circle();
$c->radius = 5;
$c->origin['x'] = 3;
$c->origin['y'] = 4;

echo 'Preparing to sleep.....';
$_SESSION['c'] = serialize($c);

echo '<br /><a href="page2.php">Wake the object</a>';
?>
```

The second file you’ll name page2.php:

```php
<?php
session_start();

class Circle
{
    public $radius;

    public $origin = array('x'=>0, 'y'=>0);

    public function __sleep()
    {
        echo 'zzzzz';

        return array('radius','origin');
    }

    public function __wakeup()
    {
        echo 'good morning!';
    }

    echo 'Rise and shine.....';

    $c = unserialize($_SESSION['c']);

    echo '<br />The contents of our Circle object are:<br />';
    echo 'Radius: ' . $c->radius . '<br />';
    echo 'Origin: (' . $c->origin['x'] . ',' . $c->origin['y'] . ')';
?>
```

Load the first page, page1.php, into your browser, and you should see something similar to Figure 2.1.

![](img/fd2e7361878181c2b12e30301ff3e182_66_0.png)

**Figure 2.1**

Click the link, and you will be directed to page2.php, where you should see something like Figure 2.2.

![](img/fd2e7361878181c2b12e30301ff3e182_67_0.png)

**Figure 2.2**

In the first file, page1.php, you start your session so you can store the object in a session variable; then you proceed to create the class definition for circle:

```php
<?php
session_start();

class Circle
{
    public $radius;

    public $origin = array('x'=>0, 'y'=>0);

    public function __sleep()
    {
        echo 'zzzzz';

        return array('radius', 'origin');
    }

    public function __wakeup()
    {
        echo 'good morning!';
    }
}
```

Note that you create the functions for both `__sleep` and `__wakeup` here. Creating the `__wakeup` method is not necessary in this case, but if you were to move the class definition to an include file later on, all you'd have to do is cut and paste. Also notice that you return an array of strings in `__sleep`. These strings match up with property names inside `Circle`, and tell the serialization functions what parts of the object you want to serialize, and to ignore all others.

You then proceed to instantiate the circle object, change some of its values, serialize it to a session variable, and finally provide a link to go to `page2.php`:

```php
$c = new Circle();
$c->radius = 5;
$c->origin['x'] = 3;
$c->origin['y'] = 4;

echo 'Preparing to sleep....';

$_SESSION['c'] = serialize($c);

echo '<br /><a href="page2.php">Wake the object</a>';
?>
```

Looking at `page2.php`, you once again start out with a call to start the session, and an identical class definition as the previous page. When unserializing an object, the class definition for that object *must* be present before the `unserialize()` function is called, either typed in the file itself, or included via the include or require statements.

Getting into the meat of `page2.php`, you unserialize the data from the session variable you set in the previous page, and echo some of the newly recreated object's properties to the screen:

```php
echo 'Rise and shine....';

$c = unserialize($_SESSION['c']);

echo '<br />The contents of our Circle object are:<br />';
echo 'Radius: ' . $c->radius . '<br />';
echo 'Origin: (' . $c->origin['x'] . ', ' . $c->origin['y'] . ')';
?>
```

### __toString

The final magic method that can be built into classes is `__toString`. As you might guess, `__toString` returns a custom string value that is automatically used when the object is converted to a string. Take the following example:

```php
<?php

class Circle
{
    public function __toString()
    {
        return "Automatic string value for Circle";
    }
}

$c = new Circle();
echo "The value of \$c is: ";
echo $c;
?>
```

This code would produce the following when executed:

> The value of $c is: Automatic string value for Circle

In this example, you added the `__toString()` magic method, and used it to provide a value when the object was echoed to the screen. Note that you didn’t simply concatenate the object on to the end of the string in the previous echo statement, or include it inside the double-quoted string.

What exactly would happen if you simply included the object with another string in a single echo statement? Look at the following code (the changes are highlighted):

```php
<?php

class Circle
{
    public function __toString()
    {
        return "Automatic string value for Circle";
    }
}

$c = new Circle();
echo "The value of \$c is: " . $c;
?>
```

When you run this code, you see the following:

> The value of $c is: Object id #1

That’s definitely not what you expected! Instead of returning the value from the `__toString()` method, it instead returned an object id for `$c` —exactly the same as you would see had you not defined `__toString()`. The `__toString()` magic method is only called when used directly with `echo` or `print` —if any other strings or casts are present, the object id will be returned instead.
