# Displaying the Values of Variables

The echo command—which we've already used to print values such as strings received from standard input—is used to display the value stored inside a shell variable. To do this, you simply

```
$variable
```

The $ character is a special character to the shell when followed by one or more alphanumeric characters. If a variable name follows the $, the shell takes this as an indication that the value stored inside that variable is to be substituted at that point. So, when you

```
echo count
```

the shell performs $count with the value stored there; then it executes the echo command:

```
$ echo $count
$
```

Remember, the shell performs variable substitution before it executes the command (see Figure 4.1).

![](bbox=[0.119, 0.452, 0.532, 0.497])

Figure 4.1 echo $count

You can have the value of more than one variable substituted at a time:

```
$ echo $my_bin
/users/steve/bin
$ echo $my_bin $count
/users/steve/bin 1
$
```

In the second example, the shell substitutes the values of my_bin and count and then executes the echo command (see Figure 4.2).

![](bbox=[0.119, 0.74, 0.532, 0.785])

Figure 4.2 echo $my_bin $count