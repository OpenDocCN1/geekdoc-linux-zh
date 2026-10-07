# Chapter 6: ADVANCED VARIABLE USAGE 287

functions. It's actually an alias for typeset -r. Because float is also an alias for a typeset command, line 6054 is equivalent to:

```
typeset -Fr two_pi=$((( 2 * 3.141592654 \))
```

If you declare a variable to be read-only, it becomes a "constant," and you eliminate the chance that you might accidentally change its value.

![](bbox=[0.105, 0.245, 0.155, 0.285])

Read-only variables are not absolutely constant. If you declare a variable that the shell changes, such as SECONDS, to be read-only, you can't change it anymore, but the shell itself still can.

```
float x y=5 z=7
print -- $(( x = sqrt(y * z), y=x/2, y=y * 4 )) $x $y $z
```

+   e) What two values are the same, and why?

Answer:Your interaction should look like the following:
[6057]: float x y=5 z=7
[6058]: print -- $(( x = sqrt(y * z), y=x/2, y=y * \ 4 )) $x $y $z
11.832159662 5.916097983 2.958039892 11.832159597
[6059]:

The first and fourth numbers have the same value. The first one is the value of the last (rightmost) assignment in the arithmetic expansion, and the fourth is the value of z, which is the variable that received the result of that same assignment.

+   f) If the two values are the same, why did they print differently?
Answer:They are the same value, but they are printed with different numbers of digits because z is declared as a float, but the expression does not have an associated precision.

# FOR EXAMPLE

You can control the number of digits used to print the value of a variable using the typeset command, but you don't have any way to control the precision when printing the results of arithmetic expansions when you,