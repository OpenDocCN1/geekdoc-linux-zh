
If the class is called *House*, Perl translates

```perl
$ref = House->new();
```

to

```perl
$ref = House::new(House);
```

### Instance Method Invocation

Assume the method name is called *display* and the reference to the object is called *$obj*.

- 1) `$obj->display( list of arguments );` # object-oriented syntax
- 2) `display $obj( list of arguments );` # indirect syntax

The example using the arrow operator to invoke a method is called the object-oriented style and is the most commonly used. We will use that style throughout this text; the example without the arrow operator is called the indirect syntax.

When Perl sees one of the preceding methods being invoked, it knows what class the object belongs to, because the object was blessed (an internal pointer is tracking where it is).⁴

If you call either

```perl
display $ref( arguments...);
```

or

```perl
$ref->display(arguments...);
```

and *$ref* points to an object in a class called *House*, Perl translates that to

```perl
House::display($ref, arguments...);
```

### Creating the Object with a Constructor.

To create a *House* class, we first create a package. This package is called *House*. In object-oriented lingo, the package will now be called a class. A function called a constructor method is used to create the object and give it a memory address so that your program can access it.

The properties, or attributes, describe characteristics of the object, such as its *owner*, *style*, *size*, *color*, and so forth. In our example, the house properties are *Owner*, *Color*, and *Payment*. There are a variety of ways to set the properties. Often, the object is described with an anonymous hash, where the key/value pairs are the properties of the object.

In the following example, the class is called *House* and the constructor method is called *new()*. You don’t have to name the constructor “new.” You can call it whatever fits your situation best. Since we’re making a new house, the name “new” seems as fitting as any other name; we could have easily used *create0*, *build0*, *startup0*, or *init0*. The job of the constructor is to set up a memory location for the new *House* object; in other words, to get a reference to the object. We can define the actual properties later, but first we need to get the address for the object, just as you have to have an address for a new house before you can build it.

Like any other function, the constructor can receive additional arguments from the caller, and use them as “instance” variables. The next step is to make sure Perl knows that this new address is always associated with its class. The new *house* object is a member of the *House* class, and the *bless* function makes sure Perl knows that. Simply, it converts the ordinary pointer into an object. The piece of memory it points to is stamped: “I’m not a Car, or a Horse, or a Cat. I am a *House*!”

Example 14.2 illustrates how to define the constructor method, create a reference, and transform it into an object via the *bless* function. At this point in the program, we are only defining the method. Later, we will invoke it.

#### EXAMPLE 14.2

```perl
package House;   # Name of the class

sub new { # The constructor method
    my $class=shift @_; # First argument is the name of the class
    my $house_obj={
        "Owner"=>"Planet Bank", # Default attributes
        "Color"=>"Beige",
        "Payment"=>undef,
    };

    bless($house_obj, $class); # Create the object by blessing it
    return $house_obj;

    # The blessing transforms the ordinary pointer into a pointer to an
    # object. The object now belongs to the House class.
}
```

### EXPLANATION

- 1. The *package House* is declared. It can be called a class because it contains a method that will bless a reference.
- 2. The subroutine *new* is called a **constructor** method in OOP lingo. The primary job of a constructor is to create and initialize an object. In Perl, it doesn’t really have any special syntax. This is called a class method, since its first argument is the name of the class which is shifted from the @_ array. (See Example 14.4 to see how this method is invoked.) It is a subroutine that blesses a referenced “thing” (object) into a class and returns a reference to it. The subroutine is called a **method** and the “thing” it blessed is an **object**. The *package* is called a **class**.
- 3. The first argument received by this type of subroutine is the name of the package or class, in this case House. This is another difference between a method and a subroutine. The first argument of a method is the name of either a class or an object.
- 4. The reference $house_obj is assigned the address of an anonymous hash (object). There are three keys with values. The value of “Payment” is assigned undef, meaning the values at this time are undefined and will be defined later. These key/value pairs serve as default attributes/properties for the house object. You could leave the hash empty and set the properties later, for example, $house_obj = {}; They can be set or modified by instance methods defined in Example 14.3.
- 5. The reference $house_obj, is the first argument to the bless() function, and the name of the class is the second argument. The blessing does not bless the reference. It blesses the location that the reference points to, called the referent. It tags that location with the class name, transforming the ordinary reference into a reference to an object.
- 6. A reference to the object is returned to the caller.

### Creating the Instance Methods

Outside of the constructor method, other methods can be defined. In the object-oriented world, these methods are called public methods, and they are the way you get access to the object, but not until an instance of it exists. They often describe behaviors of the object, meaning, what it can do or what can be done to it. In fact, the methods should be the only way to get access to the object.

For our house object, one method to access the house might be to move in, another to clean it, another to display it, and so on. Methods in Perl are just glorified subroutines. In the following example, we add three instance (mutators or setters) methods to the House class. These methods, set_owner(), set_color(), and set_price() all assume that an instance of the object has already been created; in other words, you can’t own, paint, or make payments on the house if it doesn’t exist. In instance methods always get a reference to the object as their first argument. Once the method has the address of the object and knows that class it belongs to (blessing), it will go to that address and perform whatever tasks it is programmed to do, such as set values, return values, change the defaults, for example, calculate the mortgage, add a garage, clean the kitchen, tear it down, and so forth.

#### EXAMPLE 14.3

```perl
package House;    # Name of the class

sub new{
   my $class=shift;
   my $house_obj={  "Owner"=>"Planet Bank",      # Default attributes
                   "Color"=>"Beige",
                   "Payment"=>undef,
                  };
   return bless($house_obj, $class);
}
#------------------------

# Create the instance methods that will manipulate the object
# The setter methods
sub set_owner{    # Access or instance methods
    my ($self, $owner) = @_;
# First argument is a pointer to the house object
    $self->{"Owner"}=$owner;    # Set a new owner
}
sub set_color{    # Setter method
    my ($self,$color) = @_;
# First argument is a pointer to the house object.
    $self->{"Color"}=$color;
}
sub set_payment{
    my ($self, $payment) = @_;
# First argument is a pointer to the house object
    $self->{"Payment"}=$payment;
}
# The getter methods
sub get_owner{
    my $self=shift;
        return $self->{"Owner"};
}
sub get_color{
    my $self=shift;
        return $self->{"Color"};
}
sub get_payment{
    my $self=shift;
        return $self->{"Payment"};
}
```

### EXPLANATION

- 1. The class is House.
- 2. The constructor is defined with default properties.
- 3. The instance methods are defined here. This is the set_owner method, called a “setter” (mutator). It stores the data in the object.
- 4. The first argument received by the set_owner method is a reference to the object. It is called $self. $self is commonly used, but the method can be called any valid variable name. The second argument is the value of the Owner property for the object. When the method is called by the user, Perl implicitly sends a reference to the object first and then any other arguments sent by the user.
- 5. A reference to the object is stored in $self. The value of the Owner property is assigned to the object via this reference.
- 6. This method is called a “getter.” It retrieves (gets) information from the object. The first argument is the address of the object, $self.
- 7. The value of the Owner property is retrieved and returned to the user.
