the flow of execution of the statements. You already have seen the `if` statement and a `while` loop. Perl includes a complete set of flow-control statements just like those in C, but with a few extra features.

In Perl, all conditional statements take the following form:

```
```perl
conditional-statement
{ Perl code to execute if conditional is true }
```
```

Notice that you must enclose within braces `{...}` the code that follows the conditional statement. The conditional statement checks the value of an expression to determine whether to execute the code within the braces. In Perl, as in C, any nonzero value is considered logically true, whereas a zero value is false.

Next I briefly describe the syntax of the major conditional statements in Perl.

# ### if and unless

The Perl `if` statement resembles the C `if` statement. For example, an `if` statement may check a count to see whether the count exceeds a threshold, as follows:

```
```perl
if ($count > 25) { print "Too many errors!\n"; }
```
```

You can add an `else` clause to the `if` statement, like this:

```
```perl
if ($user eq "root")
{
    print "Starting simulation...\n";
}
else
{
    print "Sorry $user, you must be '\\root' to run this
program.\n";
    exit;
}
```
```

If you know C, you can see that Perl's syntax looks quite a bit like that in C. Conditionals with the `if` statement can have zero or more `elsif` clauses to account for more alternatives, as in the following code:

```
```perl
print "Enter version number:"; # prompt user for version number
$os_version = <STDIN>;    # read from standard input
chop $os_version; # get rid of the newline at the end of the line
# Check version number
if ($os_version >= 10) { print "No upgrade necessary\n";}
elsif ($os_version >= 6 && $os_version < 9)
    { print "Standard upgrade\n"; }
elsif ($os_version > 3 && $os_version < 6) { print "Reinstall\n";}
else { print "Sorry, cannot upgrade\n";}
```
```