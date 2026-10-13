Other integer operators behave similarly, so

```
```sh
[ "$choice" -lt 5 ]
```
```

tests to see whether the variable choice is less than 5.

The command

```
```sh
[ "$index" -ne "$max" ]
```
```

tests to see whether the value of index is not equal to the value of max.

Finally

```
```sh
[ "$#" -ne 0 ]
```
```

tests to see whether the number of arguments passed to the command is not equal to zero.

It’s important to note that the test command, not the shell itself, interprets the variable’s value as an integer when an integer operator is used, so these comparisons work regardless of the shell variable’s type.

Let’s have a closer look at the difference between test’s string and integer operators with a few examples.

```
```sh
$ x1="005"
$ x2="10"
$ [ "$x1" = 5 ]             String comparison
$ echo $?
1                           False
$ [ "$x1" -eq 5 ]            Integer comparison
$ echo $?
0                           True
$ [ "$x2" = 10 ]             String comparison
$ echo $?
1                           False
$ [ "$x2" -eq 10 ]           Integer comparison
$ echo $?
0                           True
$
```
```

The first test

```
```sh
[ "$x1" = 5 ]
```
```

uses the string comparison operator = to test whether the two strings are identical. They’re not, because the first string is composed of the three characters 005, and the second the single character 5.

In the second test, the integer comparison operator -eq is used. Treating the two values as integers (numbers), 005 is equal to 5, as verified by the test exit status.