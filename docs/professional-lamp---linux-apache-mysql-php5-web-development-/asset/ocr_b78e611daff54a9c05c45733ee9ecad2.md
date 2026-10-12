# Chapter 1

This abstract class basically says "create a calendar, but then you must specify what type in the child class." As you can see, the showCalendar() function is intentionally left blank and abstract in the first class because that class should be extended and the proper calendar shown based on the inherited class that was called. The getToday() class was incomplete, and was a perfect candidate for abstraction.

Abstract methods, like those in the interface, are effectively blank and require further implementation in child classes.

Some rules when using the abstract class include:

+   * If you have an abstract method, the entire class must be defined as abstract as well.
+   * You cannot instantiate an abstract class.
+   * You can define a class as being abstract without having any abstract methods contained in it.
+   * The inheriting classes that are implementing abstract methods must have the same (or weaker) visibility than their parents.

In Chapter 2, we discuss abstraction in greater detail.

# Built-In Method Overloading Functions

Unlike PHP4, where you had to use the overload() function to force an overload check, PHP5 natively allows you to overload any method or member reference that is not what is expected, thus effectively giving you control over what happens next. The new magic methods \_\_get(), \_\_set(), and \_\_call() are used in overloading, as follows:

```
```php
<?php
class overload {

    function \_\_get($property) {
        //check to see if the property exists within the class
        //and if not, do something we want it to
        //such as show an error. Otherwise return
        //a value.
    }

    function \_\_set($property, $value) {
        //check to see if the property exists within the class
        //and if it does, set it to the value being passed
        //otherwise do something we want it to, such
        //as show an error.
    }

    function \_\_call($method, $array_of_arguments) {
        //check to see if method exists within the class
        //and if not, do something such as defer it to
        //another class containing the method or
        //print an error statement.
    }
}
```
```