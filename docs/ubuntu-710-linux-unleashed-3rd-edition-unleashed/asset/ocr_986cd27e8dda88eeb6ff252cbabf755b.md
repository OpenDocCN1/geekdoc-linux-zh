# foreach

The foreach construct performs a statement block for each element in a list or array:

```
@names = ("alpha", "bravo", "charlie");
foreach $name (@names) {
    print "$name sounding off!\n";
}
```

The loop variable ($name in the example) is not merely set to the value of the array elements; it is aliased to that element. That means if you modify the loop variable, you're actually modifying the array. If no loop array is specified, the Perl default variable $_ may be used:

```
@names = ("alpha", "bravo", "charlie");
foreach (@names) {
    print "$_ sounding off!\n";
}
```

This syntax can be very convenient, but it can also lead to unreadable code. Give a thought to the poor person who'll be maintaining your code. (It will probably be you.)

> NOTE
> foreach is frequently abbreviated as for.

# while

while performs a block of statements as long as a particular condition is true:

```
while ($x<10) {
    print "$x\n";
    $x++;
}
```

Remember that the condition can be anything that returns a true or false value. For example, it could be a function call:

```
while ( InvalidPassword($user, $password) ) {
    print "You've entered an invalid password. Please try again.\n";
    $password = GetPassword;
}
```