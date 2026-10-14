```
Price paid? 54.67
Tax rate (ex: .06)? .06
List price = $ 51.58
Tax paid = $ 3.09
```

Press Enter and examine the calculated list and tax variables with print commands:

```
(gdb) print list
$3 = 51.575471698113212
(gdb) print tax
$4 = 3.0945283018867897
```

If the values surprise you, remember that floating point binary values are best considered to be approximations. Only integers are perfectly accurate at all times. Floating point values are subject to round-off errors, which though extremely small, might adversely affect program results. For this reason, in accounting and similar software, it might be more appropriate to store monetary values in variables of type long or long long.

# AUTOMATICALLY DISPLAYING VARIABLES

To automatically display expressions such as the values of selected variables every time the program pauses, use a display command and specify the variables to inspect. The following commands tell the debugger to display the values of list and tax every time it pauses the program—when a breakpoint is reached, for example, or when you issue a next command:

```
(gdb) display list
1: list = 51.575471698113212
(gdb) display tax
2: tax = 3.0945283018867897
```

As the following screen output shows, running the program to a breakpoint now automatically displays the values of the two variables:

```
Breakpoint 1, main () at tax.cpp:28
28 return 0;
2: tax = 3.0945283018867897
1: list = 51.575471698113212
```

# ASSIGNING VALUES

Use the gdb set command to assign values to a program's variables. This is often handier for supplying test data for calculations than rerunning the program from scratch. For example, to set the rate variable in tax.cpp to 0.075, use the following command followed by print to verify the new value:

```
(gdb) set rate = 0.075
(gdb) print rate
$6 = 0.07499999999999997
```

Notice that the internal binary representation of 0.075 is a close approximation.