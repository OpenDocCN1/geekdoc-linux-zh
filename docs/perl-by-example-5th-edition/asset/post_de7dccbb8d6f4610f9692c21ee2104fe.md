
## EXAMPLE 14.1 (CONTINUED)

```perl
(Output)
The owner of my first house is Planet Bank
$VAR1 = bless( {
  'Owner' => 'Planet Bank',
  'Payment' => undef,
  'Color' => 'Beige'
}, 'House' );
$VAR2 = bless( {
  'Owner' => 'Mr. T',
  'Payment' => 2000,
  'Color' => 'Beige'
}, 'House' );
```

# A Perl Package Is a Class.

A Perl package serves as a class. There is no reserved word called *class*, but with object-oriented Perl, a package is often called a class. A class is normally stored in a *pm* module, and the class name is the same as the module (minus the *.pm* extension). If you *want* to distinguish between the two terms, a class is a package containing special subroutines called methods that create and manipulate an object. A Perl class normally consists of the following:

- 1. The data that describes the object.
- 2. A constructor method that creates the object with a `bless` function.
- 3. Special subroutines, called “methods,” that know how to create, access, manipulate, and destroy the object.

There are *no* special Perl keywords such as *private*, *public*, or *protected* as in other object-oriented languages. Perl’s package mechanism makes up the class where the data and subroutines, called methods, are stored. The *my* function keeps variables lexically scoped, and the *bless* function guarantees that when the object is created, it will know to which class it belongs. In summary, the object is a reference to an anonymous hash, array, scalar, or subroutine and is manipulated by special functions called methods that get access to the object via the reference.

# A Perl Class.

Since a class is really just a package, it has its own symbol table, and the global data or routines in one class can be accessed in another.

Unlike other languages, Perl does not strictly monitor public/private borders within its modules.* To keep data private, there are several techniques that can be used (see Section 14.3, “Anonymous Subroutines, Closures, and Privacy,” later in this chapter).

![](img/8556abcb353c0991f12099420ec28735_483_0.png)

## 14.2.3 Perl Objects

**References.** To begin with, an object in Perl is created by using a reference. You may want to review Chapter 12, “Does This Job Require a Reference?” If you are not clear about how to use references. Briefly, a reference is a scalar that holds the address of some variable. A reference might also point to a data type that has no name, called an **anonymous variable**. For example, here is a reference, called $ref, to an anonymous hash consisting of two key/value pairs:

```perl
my $ref=["Owner"=>"Tom", "Price"=>"25000"];
```

To access a value in the anonymous hash, the reference (pointer) $ref can be dereferenced by using the arrow operator, as follows:

```perl
$ref->{"Owner"}
```

To make a Perl object, first a reference is created. The reference is often to an anonymous hash (although it could be assigned the address of an array or scalar or even a subroutine). The hash will contain the data members and properties of the object.

**The Blessing.** The memory address referenced (called a **referent**), must be “blessed” in order to transform it into a Perl object; in other words, the referent must know what package it belongs to. This is done by creating the reference and then blessing (the thing it references) into a package. Think of the blessing as creating a new data type, an object.

```perl
my $ref= (Owner=>"Tom", Price=>250000); # Properties Owner, Price
bless($ref, "House"); # Tag the reference as belonging to a House
return $ref; # A reference to the object is returned to the caller
```

The *bless* function takes one or two arguments. The first argument is *always* a reference, and the second optional argument is the name of the class (package). The *bless* function tags the thing being referenced (called a referent). It creates an internal pointer to track what package the thing (object) belongs to. The object is the thing (usually a hash) that was blessed into the class (package). If the *package* is not listed as the second argument, the *bless* function assumes the current package.

The *bless* function returns a reference to the blessed object. In the Figure 14.2, the address of the object is displayed before the blessing and after the blessing. Notice that after the blessing, the address is tagged with the name of the class, in this example *House*.

![](img/8556abcb353c0991f12099420ec28735_484_0.png)

### Figure 14.2 An address before and after the blessing.

Since the blessing associates the object with a particular package (class), Perl will always know to what package the object belongs, eliminating the need to use the `::` syntax we used in the procedural modules. An object can be blessed into one class and then *reblessed* into another and then another, and so on, but an object can belong to only one class at a time. Once an object has been blessed, you don’t have to export symbols with the `@EXPORT_OK` or `@EXPORT` arrays. In fact, as a general rule, if the module is trying to be object-oriented, then export nothing.

## 14.2.4 Methods Are Perl Subroutines

**Definition.** A method is a subroutine that works with objects. For example, it is used to create an object, store or modify data in an object, retrieve data from the object, and so on. It is a special subroutine that belongs to a class, and its first argument will be one of the following:

- 1. A class (package) name
- 2. A reference to an object

This first argument is sent by Perl implicitly. Even though you may call a method without any arguments, Perl will automatically send one, either a package name or object reference. Otherwise, it looks like any other subroutine. In Example 14.1, we created two house objects. The method to create the objects was called new (although it could be called anything) and as you can see next, when the method is called, it is preceded by the class name, House, followed by an arrow, House->new(). Perl will automatically send what is on the left-hand side of the arrow to the method. So in this case, the new() method will automatically get one argument, which is House, the class name.

- 1. Perl implicitly sends the name of the class to the new() method

![](img/8556abcb353c0991f12099420ec28735_485_0.png)

```perl
$house1 = House->new(); # Make a new house object and get back its address
$house2 = House->new(); # Make another house object
```

Although the parameter list for the new method is empty, Perl will implicitly send what is on the left-hand side of the arrow to the method; in this case, House (the name of the class) is sent to new() as its first argument.

- 2. Perl sends a reference to the second house, $house2, to the set_owner() method.

```perl
$house2->set_owner("Mr. T"); # Perl sends the address of the second
# house as the first argument to set_owner()
# and "Mr. T" as the second argument
```

The first argument in the set_owner() method appears to be "Mr. T" but it's not. The first argument in this method is a reference to the second house object, $house2. Notice this time, the reference is on the left-hand side of the arrow rather than the class name. Perl will implicitly send the reference as the first argument to this method, and "Mr. T" as the second. In that way, you can be assured that when you set the owner for the second house, Perl will know which address to go to.

**Types of Methods.** Now that we’ve had a brief introduction, let’s learn a little more about methods. There are two types of methods: class (or static) methods and instance methods.¹ The class method expects a class name as its first argument, and the instance method expects an object reference as its first argument.

A class method is a subroutine that affects the class as a whole; for example, it can create an object or act on a group of objects. It is independent; meaning, it doesn’t require an object as its first argument. A counter function to keep track of the number of objects created within a class, can be considered a class method. Another example of a class method is a constructor. In object-oriented programs, a constructor is a class method used to create an object and receives the class name as its first argument. In Perl, this method is commonly called `new`, although you can call it anything you like. The creation of the object is often called the **instantiation** of the object, or instance of the class.

Object-oriented programs use *instance methods* (also called access or mutator methods) to control the way the object’s data is assigned, modified, and retrieved. You can’t use an instance method until you have created the object. Once the reference to the newly created object is returned, the instance method uses that reference, often called `$this` or `$_self`, to manipulate the object. The instance method automatically receives a reference to the object as its first argument. In that way, it knows which object to manipulate; for example, when invoking a speak method, `$dog->speak()` gets a dog reference and might return “Woof woof”, whereas `$cat->speak()` gets a cat reference and might return “Meow”. Perl sends the reference for you.

**Invoking Methods.** Perl provides a special syntax for invoking methods. Instead of using the `package::function` syntax, methods are invoked in one of two ways: class method invocation or instance method invocation. There are two types of syntax for each method call: object-oriented syntax (shown in all the examples in this chapter) and indirect syntax. If you are using objects, either syntax for these method calls is acceptable, but the object-oriented syntax is less ambiguous. The older way of calling methods with the double colons is not recommended.

**Something to remember:** a method, unlike an ordinary subroutine, is always sent one argument implicitly, either the name of the class or a reference to the object. If, for example, you call a method with three arguments, four arguments are really sent, the first one being the *value* found on the left-hand side of the arrow when using the object-oriented style.

# Class Method Invocation

Assume the method name is called `new` and the return value, `*ref*`, is a pointer to the object.

- 1) `$ref = class->new ( list of arguments ); # object-oriented syntax`
- 2) `$ref = new class ( list of arguments ); # indirect syntax`
