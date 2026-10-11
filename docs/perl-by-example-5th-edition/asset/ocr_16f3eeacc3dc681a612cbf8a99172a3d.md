The user of the module, must designate the module to be included with the use Module directive, also discussed in Chapter 13. There are many ways the module can be designed. This is just one simple approach.

```
The Module Filename: House.pm

package House;  # House is the class
# The package name normally matches the filename minus the .pm extension

sub new{
    my $class = shift;     # Constructor method
                           # First argument is the name of the class
    my $house_obj = { };   # Create the reference/pointer.
    bless($house_obj, $class); # Bless the referent; Create an object
    return $house_obj;       # Return a reference to the object
}

sub set_owner{
    my $Self = shift; # Access/instance method
                      # First argument is a reference to the object
    $Self->("Owner")=shift; # Sometimes called a "setter" method
}

sub get_owner{
    my $Self = shift; # Access/instance method
                      # First argument is a reference to the object
    return $Self->("Owner"); # Sometimes called a "getter" method
}

1; # Must return a true value, or module won’t load
```

```
The user of the Class: the Perl script, myHouse.plx

use House; # Tell Perl to load House.pm

my $house1 = House->new(); # Call class constructor.
# Get back a reference to a new house. Perl sends
# the name of the class as its first argument

my $house2 = House->new(); # Create another house object

$house1->set_owner("B of A"); # Call access method:
# Perl sends the address of the first house
# object, to method set_owner()

print "The owner of the first house is ", $house1->get_owner, "\n";
# Perl gets the object's data with the get_owner access method
```

![](bbox=[0.03, 0.89, 0.5, 0.92])