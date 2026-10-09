You can then incorporate the module in a Perl program. The following example uses the timestamp module to generate a unique filename:

```
$ cat fn.pl
use Timestamp::Simple qw(stamp);

# Save timestamp in a variable
$ts = stamp, "\n";

# Strip off the year
$ts =~ s/...(.*)/^1/;

# Create a unique filename
$fn = "myFile." . $ts;

# Open, write to, and close the file
open (OUTFILE, ">", "$fn");
print OUTFILE "Hi there.\n";
close (OUTFILE);

$ perl fn.pl
$ ls myf*
myFile.0905183010
```

substr  You can use the substr function in place of the regular expression to strip off the year. To do so, replace the line that starts with $ts =~ with the following line. Here, substr takes on the value of the string $ts starting at position 4 and continuing to the end of the string:

```
$ts = substr ($ts, 4);
```

# EXAMPLES

This section provides some sample Perl programs. First try running these programs as is, and then modify them to learn more about programming with Perl.

The first example runs under Linux and displays the list of groups that the user given as an argument is a member of. Without an argument, it displays the list of groups that the user running the program is a member of. In a Perl program, the %ENV hash holds the environment variables from the shell that called Perl. The keys in this hash are the names of environment variables; the values in this hash are the values of the corresponding variables. The first line of the program assigns a username to $user. The shift function (page 1055) takes on the value of the first command-line argument and shifts the rest of the arguments, if any remain. If the user runs the program with an argument, that argument is assigned to $user. If no argument appears on the command line, shift fails and Perl executes the statement following the Boolean OR (||). This statement extracts the value associated with the USER key in %ENV, which is the name of the user running the program.