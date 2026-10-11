# Chapter 13 • Modularize It, Package It, and Send It to the Library!

The double colons are reminiscent of the C++ scope resolution operator. When referring back to the main package from another package, you can omit the name of the package. Instead of :main::friend, you could say ::friend. To reference a subroutine in another package where, for example, the package name is Dog, a call to a subroutine from another package might be as follows:

```
Dog::play("catch")
Dog::sit()
```

In the following example, you will see package declarations within the same file, their scope, and how to switch from one package to the other.

# EXAMPLE 13.2

```
1 package Dog; # Package declaration
2 our $name="Lassie"; # Package variable
3 my $gender="female"; # Lexical private variable
4 @treats=("rawhide", "pork bone", "bacon twists", "milkbone" );
5 sub play{
my $dogname = shift;
print "$dogname catches a tennis ball.\n";
}
6 package Cat; # Package declaration
7 $name = "Skiddy";
8 print "Treats are: @treats\n"; # Not defined in this package
9 print "$name says hello to $Dog::name.\n";
10 print "$Dog::name is a $Dog::gender.\n";
11 print "$name prefers chicken flavored Temptations\n";
12 print "$Dog::name loves ",join(", ", @Dog::treats),
" but prefers $Dog::treats[0].\n";
13 Dog::play($name); # Call function in package Dog
```

(Output)
8 Treats are:
9 Skiddy says hello to Lassie.
10 Lassie is a .
11 Skiddy prefers chicken flavored Temptations
12 Lassie loves rawhide, pork bone, bacon twists, milkbone but prefers rawhide
13 Skiddy catches a tennis ball.