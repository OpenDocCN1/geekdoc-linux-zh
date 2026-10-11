11.2 Passing Arguments and the @_ Array

# 11.2.9 Autoloading

The Perl AUTOLOAD function is called whenever Perl is told to call a subroutine and the subroutine can't be found. The special variable $AUTOLOAD is assigned the name of the undefined subroutine.

You can also use the AUTOLOAD function with objects to provide an implementation for calling unnamed methods. (A *method* is a subroutine called on an object.)

```
EXAMPLE 11.20

```perl
(The Script)
use warnings;
sub AUTOLOAD {
    my (@arguments)=@_;
    my $args=join(', ', @arguments);
    print "$AUTOLOAD was never defined.\n";
    print "The arguments passed were $args.\n";
}

my $driver="Jody";
my $miles=50;
my $gallons=5;

$mileage($driver, $miles, $gallons); # Call to an undefined
                                      # subroutine
(Output)
main::mileage was never defined.
The arguments passed were Jody, 50, 5.
```
```

+   EXPLANATION
+   1. The subroutine AUTOLOAD is defined.
+   2. The AUTOLOAD subroutine is called with the same arguments as would have been passed to the original subroutine called on line 7.
+   3. The arguments are joined by commas and stored in the scalar $args.
+   4. The name of the package and the subroutine that was originally called are stored in the $AUTOLOAD scalar. (For this example, main is the default package.)
+   5. The arguments are printed.
+   6. The scalar variables are assigned values.
+   7. The mileage subroutine is called with three arguments. Perl calls the AUTOLOAD function if there is a call to an undefined function, passing the same arguments as would have been passed in this example to the mileage subroutine.