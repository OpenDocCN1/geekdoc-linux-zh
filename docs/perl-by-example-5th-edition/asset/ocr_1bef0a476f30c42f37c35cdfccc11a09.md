other name; we could have easily used *create0*, *build0*, *startup0*, or *init0*. The job of the constructor is to set up a memory location for the new *House* object; in other words, to get a reference to the object. We can define the actual properties later, but first we need to get the address for the object, just as you have to have an address for a new house before you can build it.

Like any other function, the constructor can receive additional arguments from the caller, and use them as “instance” variables. The next step is to make sure Perl knows that this new address is always associated with its class. The new *house* object is a member of the *House* class, and the *bless* function makes sure Perl knows that. Simply, it converts the ordinary pointer into an object. The piece of memory it points to is stamped: “I’m not a Car, or a Horse, or a Cat. I am a *House*!”

Example 14.2 illustrates how to define the constructor method, create a reference, and transform it into an object via the *bless* function. At this point in the program, we are only defining the method. Later, we will invoke it.

# EXAMPLE 14.2

```
```
package House;   # Name of the class

sub new { # The constructor method

    my $class=shift @_; # First argument is the name of the class
    my $house_obj={
        "Owner"=>$"Planet Bank", # Default attributes
        "Color"=>"Beige",
        "Payment"=>undef,
    };

    bless($house_obj, $class); # Create the object by blessing it
    return $house_obj;

    # The blessing transforms the ordinary pointer into a pointer to an
    # object. The object now belongs to the House class.
}
```
```

# EXPLANATION

+   1. The *package House* is declared. It can be called a class because it contains a method that will bless a reference.

+   2. The subroutine *new* is called a **constructor** method in OOP lingo. The primary job of a constructor is to create and initialize an object. In Perl, it doesn’t really have any special syntax. This is called a class method, since its first argument is the name of the class which is shifted from the @_ array. (See Example 14.4 to see how this method is invoked.) It is a subroutine that blesses a referenced “thing” (object) into a class and returns a reference to it. The subroutine is called a **method** and the “thing” it blessed is an **object**. The *package* is called a **class**.