Looping constructs can either perform a block of code as long as certain conditions apply, or while they step through a list of values, perhaps using that list as arguments.

Perl has four looping constructs: for, foreach, while, and until.

# for

The for construct performs a *statement* (block of code) for a set of conditions defined as follows:

```
```plaintext
for (start condition; end condition; increment function) {
    statement(s)
}
```
```

The start condition is set at the beginning of the loop. Each time the loop is executed, the increment function is performed until the end condition is achieved. This looks much like the traditional for/next loop. The following code is an example of a for loop:

```
```perl
for ($i=1; $i<=10; $i++) {
    print "$i\n"
}
```
```

# foreach

The foreach construct performs a statement block for each element in a list or array:

```
```perl
foreach $name (@names) {
    print "$name\n"
}
```
```

The loop variable ($name in the example) is not merely set to the value of the array elements; it is aliased to that element. This means that if you modify the loop variable, you are actually modifying the array.

If no loop array is specified, as in the following example, the Perl default variable $_ is used:

```
```perl
for (@names)         {
    print "$_ was here!\n";
}
```
```

This syntax can be very convenient, but it can also lead to unreadable code. Give a thought to the poor person who will be maintaining your code. It will probably be you.

> > **Note**
> >
> > *foreach is frequently abbreviated as for.*