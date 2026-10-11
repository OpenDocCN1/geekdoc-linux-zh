# EXPLANATION

+   1.  Declare the package *House*.
+       2.  Load *Moose*. It will create the class and attributes.
+       3.  The *'color'* attribute is read/write and a *Str* (string) type.
+       4.  The *'owners'* attribute is also read/write.
+       5.  The value assigned to the *'owners'* attribute must be an array reference where each of the elements in the array will be of type *Str*. If you try to assign something other than an array reference to the *'owners'* attribute, Moose will throw an exception such as:
+   
+           ```
+           # Attribute 'owners' does not pass the type constraint because:
+           Validation failed for 'ArrayRef[Str]' with value Mr. Trump at /usr/
+           local/ActivePerl-5.16        /lib/Moose/Meta/Attribute.pm line 1274.
+           ```
+   
+       6.  Normally all attributes are optional. With the *required* attribute set to 1, Moose says the attribute *'owners'* must be provided when the constructor is called, but does not say what its values should be.
+       7.  You can explicitly specify the method name to be used for reading and writing the value of an attribute by using the *reader* and *writer* attribute options. Since the *'price'* attribute is read only, we can't directly set the price. If you want to use it to set the value of the price, you would call the *\_set\_price* method defined on line 8 as a *writer* method. The leading underscore indicates that this is a private method even though it can be called from outside the class.
+       8.  The *\_set\_price* method is defined. Even though the *'price'* attribute was defined as a read-only accessor, we can treat it as a writer accessor by using this method.

Example C.6 shows the user of the *House* module, *house.pl*.

# EXAMPLE C.6

```
```perl
#!/usr/bin/env perl
use Data::Dumper;
use strict;
use warnings;
1 my $h1 = House->new('owners'=>[ "Mrs. A", "Mr. B" ]);
2 my $h2 = House->new('owners'=>[ ]);  # Define values later
3 my $h3 = House->new('owners'=> "Mr. Trump");
4 $h1->color('red');
   $h1->_set_price(125000);
5 $h2->owners(['Mr. Trump', 'Mr. Mellon', 'CityBank']);
   $h2->color('blue');
   $h2->_set_price(5000000);

say "The price is ", $h1->price;
6 say "The owners are ", join(' ', @{$h1->owners});
say "The color is ", $h1->color;
say "The price is ", $h2->price;
```
```