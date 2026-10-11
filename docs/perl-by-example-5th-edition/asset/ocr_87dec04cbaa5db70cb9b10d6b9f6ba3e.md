If the class is called *House*, Perl translates

```
$ref = House->new();
```

to

```
$ref = House::new(House);
```

# Instance Method Invocation

Assume the method name is called *display* and the reference to the object is called *$obj*.

+   1) $obj->display( list of arguments ); # object-oriented syntax
+   2) display $obj( list of arguments ); # indirect syntax

The example using the arrow operator to invoke a method is called the object-oriented style and is the most commonly used. We will use that style throughout this text; the example without the arrow operator is called the indirect syntax.

When Perl sees one of the preceding methods being invoked, it knows what class the object belongs to, because the object was blessed (an internal pointer is tracking where it is).⁴

If you call either

```
display $ref( arguments...);
```

or

```
$ref->display(arguments...);
```

and *$ref* points to an object in a class called *House*, Perl translates that to

```
House::display($ref, arguments...);
```

# Creating the Object with a Constructor.

To create a *House* class, we first create a package. This package is called *House*. In object-oriented lingo, the package will now be called a class. A function called a constructor method is used to create the object and give it a memory address so that your program can access it.

The properties, or attributes, describe characteristics of the object, such as its *owner*, *style*, *size*, *color*, and so forth. In our example, the house properties are *Owner*, *Color*, and *Payment*. There are a variety of ways to set the properties. Often, the object is described with an anonymous hash, where the key/value pairs are the properties of the object.

In the following example, the class is called *House* and the constructor method is called *new()*. You don’t have to name the constructor “new.” You can call it whatever fits your situation best. Since we’re making a new house, the name “new” seems as fitting as any