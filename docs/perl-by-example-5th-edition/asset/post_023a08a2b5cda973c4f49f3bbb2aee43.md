
## EXPLANATION

- 1 The package `House` is declared. (At this point, the program has not provided any instructions describing what this class does or how to use it. Documentation explaining how to use a class is called the public interface. See Section 14.5, “Plain Old Documentation—Documenting a Module,” for instructions on how to document your modules the Perl way.)
- 2 The class method `new` is defined as a constructor.
- 3 The first argument to the class method is the name of the class (package).
- 4 The “instance variables” are created from the remainder of the `@_` array.
- 5 The address of an anonymous hash is assigned to the reference `$ref`. The keys are hard coded and the values are supplied from the instance variables.
- 6 The “thing” the reference `$ref` points to is blessed into the class and becomes the new object.
- 7 The value of the reference `$ref` will be returned when the method is called. The sub-routine `display_object` is an instance method. It is defined in this class.
- The first argument to the instance method is the reference to the object.
- 8 The `foreach` loop is used with the `keys` function to get the keys from the hash (object) referenced by `$self`, and in the block of the loop to print both keys and values.
- 9 The user of the class loads `House.pm` into his namespace.
- 10 The `new` method is called with three arguments. `House`, `Tom Savage`, and `250000`. The first argument is the name of the class. You don’t see it, but Perl implicitly sends it to the constructor. The next two arguments are sent explicitly by the user of the class. The only requirement here is that the `Owner` value is the first argument and the `Price` value is the second argument. There is no error checking. The example simply shows how to pass arguments to a constructor. A reference to a new `House` object is returned and assigned to `$house1`, a reference to a hash.
- 11 The `new` method is called again with different arguments, `Devin Quigley` and `55000`. The value returned to `$house2` is a reference to another object. The `new` method has been used to create two `House` objects. You can create as many objects as you want. They will all have unique addresses, as shown in the output at line 14. Since the objects were blessed in the constructor, Perl knows that the objects are in the `House` class.
- 12 The instance method is called to display the data for the object referenced by `$house1`.
- 13 The instance method is called again but to display the data of the object referenced by `$house2`.
- 14 The addresses of the two objects are printed. You can see that the addresses have been tagged as belonging to the `House` class.

### Passing Parameters to Instance Methods.
The first argument to an instance method is always a reference to the object. In the called method, this value is typically shifted from the `@_` array and stored in a variable called `$self` or `This`, although it doesn’t matter what you call the variable. The remaining arguments are then processed as they are in any regular subroutine.

The following example demonstrates an instance method that is sent additional arguments when called.

## EXAMPLE 14.6

```perl
#!/bin/perl
# Program to demonstrate passing arguments to an instance method.
# In this example, a pointer to an array is passed.
1  package House;  # Class
use warnings;
sub new{  # Constructor
    my $class = shift;
    my $ref = {};  # Define properties later
    return bless ($ref, $class);
}
3  sub set_props{  # Instance methods
4  my $object = shift;  # Pointer to object
5  my $val_ptr=shift;  # Receive another pointer
6  my ($owner,$price,$style) = @{$val_ptr};  # Create a slice
7  $object->{"Owner"}=$owner;
    $object->{"Price"}=$price;
    $object->{"Style"}=$style;
}
8  sub get_owner{
    my $self=shift;
    return $self->{"Owner"};
}
sub get_price{
    my $self=shift;
    return $self->{"Price"};
}
sub get_address{
    my $self=shift;
    return $self->{"Address"};
}
9  sub display_props{
    my $self = shift;
10 print "Properties for the ", ref($self), " are:\n";
11 foreach my $key (keys %{$self}){  # Dereference hash ref
        my $value = $self->{$key};
        printf "%-10s %-10s\n", $key, $value;
    }  # Don't forget this!
}

# (The Script)
12 use House;
use warnings;
use strict;
```

## 14.2 Perl Classes, Objects, and Methods—Relating to the Real World

### EXAMPLE 14.6 (continued)

```perl
13 my $h1 = House->new();
14 my $h1->set_props( { "Unity Bank", "12 Main St.", "150000" } );
   $h1->display_props();
   my $h2 = House->new();
15 $h2->set_props( { "Pierre Dupont", "150000", "Pacific Ridge" });
   $h2->display_props();
```

#### (Output)

```text
Owner Unity Bank
Address 12 Main St.
Price 150000

Owner Pierre Dupont
Address 10 Pacific Ridge
Price 150000
```

### EXPLANATION

- 1 The `House` class is declared.
- 2 The `new` method is a constructor. The object is an empty anonymous hash. The key/value pairs, the properties, or attributes, of the object will be assigned later. The object, referenced by `$ref`, is blessed into the `House` class.
- 3 The instance method `set_props` is defined.
- 4 The first argument is a reference to a `House` object. It is shifted from the `@_` array and assigned to `$object`. The name of the reference could be `$his` or `$self`. It doesn't matter.
- 5 The second argument is shifted from the `@_` array. It is a reference to an array.
- 6 The reference, `$val_ptr`, is dereferenced to get a list of the values passed to this method.
- 7 The values passed to the method are now assigned to the object.
- 8 The instance methods for retrieving values from the object are defined.
- 9 The selected values from the hash are printed.
- 10 The built-in `ref` function, when given an object as its argument, returns the name of the class where the object was created.
- 11 Since the object is a reference to a hash, we dereference it, `%%$self`, to get to its key/value pairs. The user of the class then loads the module into his program.
- 13 A call to the constructor `new()` returns a newly blessed house.

## Named Parameters and Data Checking.

All of the examples so far have used a *House* object. In the next example, we will create an *Employee* object. The *Employee* constructor will take parameters to be used as properties of an employee. If a constructor method is expecting a name, address, and salary to be passed in that order, it would be a problem if the arguments were sent in the wrong order, causing the address to be assigned to the name, or the name to the salary, and so on. One way to prevent that would be to pass arguments as a hash when calling methods. In this way when received by the method as parameters, they will be in the form of key/value pairs. (Of course, spelling the expected keys incorrectly could be a problem.) The following example demonstrates how to use named parameters.

### EXAMPLE 14.7

```perl
# User of Employee.pm--See Example 14.8 for module
use Employee;
use warnings;
use strict;
my ($name, $extension, $address, $basepay, $employee); # Declare my variables

print "Enter the employee's name. ";
chomp ($name=<STDIN>);
print "Enter the employee's phone extension. ";
chomp ($extension=<STDIN>);
print "Enter the employee's address. ";
chomp ($address=<STDIN>);
print "Enter the employee's basepay. ";
chomp ($basepay=<STDIN>);

# Passing arguments as a hash
$employee = Employee->new( "Name"=>$name,
                          "Address"=>$address,
                          "Extension"=>$extension,
                          "PayCheck"=>$basepay,
                        );
print "\nThe statistics for $name are: \n";
$employee->get_stats;
```

#### (Output)

```text
Enter the employee's name. Daniel Savage
Enter the employee's phone extension. 2534
Enter the employee's address. 599 Mission Ave, Somewhere, CA
Enter the employee's basepay. 2200

The statistics for Daniel Savage are:
Address = 599 Mission Ave, Somewhere, CA
PayCheck = 2200
IdNum = Employee Id not provided!
Extension = 2534
Name = Daniel Savage
```

### EXPLANATION

- 1. The `Employee.pm` module will be used by this program.
- 2. `warnings` will be issued for possible errors, and the `strict` pragma will track global and undefined variables, barewords, and so forth.
- 3. A list of lexical private variables is created.
- 4. The user of the program will be asked for the information that will be passed to the `Employee` module.
- 5. The constructor is called to pass arguments as key/value pairs; that is, a hash is passed to the constructor in the `Employee` module. A reference to the object is returned and assigned to `$employee`.
- 6. The instance method `get_stats` is called to display the employee's attributes.

In the next example, let's see how the module handles its named parameters.

### EXAMPLE 14.8

```perl
# Module Employee.pm—See Example 14.7 to use this module.
package Employee;
use Carp;

sub new {
    my $class = shift;
    my ($params) = @_; # Receiving the hash that was passed
    my $ref = {
        "Name" => $params{"Name"} || croak("No name assigned"),
        "Extension" => $params{"Extension"},
        "Address" => $params{"Address"},
        "PayCheck" => $params{"PayCheck"} || croak("No pay assigned"),
        ((defined $params{"_IdNum"}) ? ("_IdNum" => $params{"_IdNum"}) : croak("Employee's id was not provided!\n"))
    };
    return bless($ref, $class);
}

sub get_stats {
    my $self = shift;
    foreach my $key (keys %$self) {
        print $key, " = ", $self->{$key}, "\n";
    }
    print "\n";
}
```
