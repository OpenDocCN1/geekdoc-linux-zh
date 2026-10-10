If you omit the optional variable name that refers to the element the loop is looking at ($line in this example), use the default $_ variable name to refer to the current element. It's a good idea to specify a variable name here in order to prevent confusion when you're using multiple nested foreach loops.

for
Perl also has a standard for loop, which is almost identical to the for loop in C. The purpose of for is simply to iterate a specified number of times rather than over the elements of an array. The for loop is controlled by an iteration variable—generally one that isn't used anywhere else in the script—that is iterated automatically by for until it reaches your specified limit. Its arguments, as in C, are separated by semicolons. These include the name of the iteration variable, the incrementation operation, and the end condition. Here's an example:

```
for ($i; $i++; $i<100) {
print "$i\n";
}
```

This sample for loop will print out 100 lines, numbered from 0 to 99. The first argument sets up $i as the iteration variable, and the second says that $i should be incremented upward once. The for loop will execute unless the condition specified in the third argument is false, which in this example occurs once $i has reached 100.

while/until/ do
Finally, we have the while loop, which acts like a simplified version of for without the iteration variable. It has a conditional statement as its argument, which is evaluated every time the loop begins, and it keeps executing until the conditional is false. Here's an example:

```
while ($i < 100) {
$i += 5;
$j++;
}
print "$j\n";
```

This loop will execute 20 times, and the output of the print statement will be 20.
A variant of while is until, which has effectively the opposite meaning: It keeps executing until the conditional is true. The following example has the same effect as the previous while loop:

```
until($i == 100) {
$i += 5;
$j++;
```