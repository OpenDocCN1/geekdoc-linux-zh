# EXAMPLE 13.6 (CONTINUED)

```
print "Enter your midterm scores:\n";
my @scores=split(' ', <STDIN>);
3 printf "The average is %.1f.\n", Average:save(@$scores);
# The ave subroutine is found in a file called Average.pm
----------------------
4 $ cd mylib   # Directory where library is located
```

(The Script)

```
5 $ cat Average.pm  # File where subroutine is defined
6 package Average;   # Declare a package
use strict;
use warnings;
# Average a list of grades
7 sub ave {
8 my $graderef = shift @_; # Shift off the reference
my $num_of_grades = @$graderef; # Get the size of the list
my $total;
foreach my $grade ( @$graderef ){
$total += $grade;
}
9 return $total/$num_of_grades; # What gets returned
10} # Make sure the last statement returns true
# or use will not succeed!
```

# EXPLANATION

+   1. The *use* lib pragma prepends the \@INC array with the pathname to your personal directory, *mylib*.

+   2. The *use* function first checks the \@INC array to get a listing of all directories in which it will search for the *pm* file and if it is found, includes the Perl file *Average.pm*.

+   3. The *ave* function is called with one argument, a reference to an array, and returns a value to be stored in the scalar *Saverage*. Since the subroutine *ave()* is defined in a package called *Average* in another module, the package name (and two colons) must precede the call to *ave()*. If not, Perl will try to find *ave()* in *main*, the current package.

+   4. Now we *cd* to the directory where the module is located.

+   5. The UNIX *cat* command displays the contents of the module, *Average.pm*. (Use the *type* command for MS-DOS rather than *cat*.)

+   6. The package *Average* is declared.

+   7. The subroutine, *ave()*, in this package is defined. Remember, subroutine names are global; meaning they are stored on the symbol table for the package and accessible in another package with the :: syntax.

+   8. A reference to the array of grades is sent to the function, shifted off the \@\_ array, and assigned to a local reference, *Sgraderef*.

+   9. The average is calculated and returned to the caller.

+   10. Without the *1*, as the last statement in the module, Perl will not load the module and will complain that it "did not return a true value."