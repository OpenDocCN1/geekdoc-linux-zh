Type next and press Enter to execute the suspect statement, and then issue a print command to inspect cdegrees:

```
(gdb) next
25     cout << "Degrees Celsius == " << cdegrees << endl;
(gdb) print cdegrees
$1 = -9.444444444444446
```

Tip
Instead of typing next, you can just type n and press Enter.

The value of cdegrees definitely shows that the program is not computing the correct result, but it doesn't tell us why. In this case, a look at the expression reveals the problem to be a missing pair of parentheses:

```
(fdegrees - 32.0 * 5.0) / 9.0 //???
```

Because multiplication has higher precedence than subtraction, the first part of this expression multiplies 32.0 times 5.0 and subtracts that result from fdegrees, but the formula calls for subtracting 32.0 from fdegrees before multiplying. Sometimes, however, the problem in an expression is not so obvious. In that case, it's often helpful to divide the expression into pieces and use gdb print commands to inspect the intermediate results. For example, you might comment-out the calculation of cdegrees and replace it with temporary code such as

```
double t1 = fdegrees - 32.0;
double t2 = t1 * 5.0;
double t3 = t2 / 9.0;
```

You can then single step these statements and inspect the t1, t2, and t3 temporary variables, and in this way further investigate the cause of a faulty expression. You don't have to perform these steps now, but keep them in mind for future problems.

If you are following along, quit the debugger (type q and answer yes when prompted whether you intend to exit the running program). Fix the faulty expression by adding parentheses, changing it to the following:

```
((fdegrees - 32.0) * 5.0) / 9.0
```

Compile the modified buggy.cpp and run. You don't have to load it into the debugger. Again, enter 75.5 when prompted:

```
$ g++ buggy.cpp
$ ./a.out
*** Warning: This program has intentional bugs
Fahrenheit to Celsius conversion
Degrees Fahrenheit? 75.5
Degrees Celsius == 23.8889
```

That looks better. But just to be sure, use a hand calculator to work out the problem and verify the program's result. Enter this expression into your calculator:

```
((75.5 - 32.0) * 5.0) / 9.0
```