If you know C, you can see that Perl's syntax looks quite a bit like that in C. Conditionals with the **if** statement can have zero or more **elsif** clauses to account for more alternatives, as in the following:

```
```
print "Enter version number:";  # prompt user for version number
$os_version = <STDIN>;      # read from standard input
chop $os_version; # get rid of the newline at the end of the line
# Check version number
if ($os_version >= 10 ) { print "No upgrade necessary\n";}
elsif ($os_version >= 6 && $os_version < 6) { print "Standard upgrade\n";}
elsif ($os_version > 3 && $os_version < 6) { print "Reinstall\n";}
else { print "Sorry, cannot upgrade\n";}
```
```

The **unless** statement is unique to Perl. This statement has the same form as **if**, including the use of **elsif** and **else** clauses. The difference is that **unless** executes its statement block only if the condition is false. You can, for example, use **unless** in the following code:

```
```
unless ($user eq "root")
{
    print "You must be "root" to run this program.\n";
    exit;
}
```
```

In this case, **unless** the string **user** is **root**, the script exits.

# while

Use Perl's **while** statement for **looping** \u2014 the repetition of some processing until an existing condition becomes logically false. To read a line at a time from standard input and to process that line, you may use the following **while** loop:

```
```
while ($in = <STDIN>)
{
    # Code to process the line
    print $in;
}
```
```

If you read from the standard input without any argument, Perl assigns the current line of standard input to the \$\_ variable. Thus, you can write the preceding **while** loop as follows:

```
```
while (<STDIN>)
{
    # Code to process the line
    print \$\_;
}
```
```