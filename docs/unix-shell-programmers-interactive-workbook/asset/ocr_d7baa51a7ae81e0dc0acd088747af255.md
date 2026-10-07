# Chapter 4: Simple Variables 191

If you assigned values to city and zip after unsetting them in Question b, your results will be different from those shown here.

![](bbox=[0.015, 0.105, 0.118, 0.163])

![](bbox=[0.015, 0.185, 0.118, 0.243])

You could have combined all those commands into a single command line:

```
state=OH; set|grep -e ^city= -e state= -e ^zip=
```

This technique is somewhat more efficient than running separate commands for each variable because set and grep are each called once instead of three times. The -e option for grep is the "trick" that lets you search for several different patterns at the same time.

Uninitialize a variable name y (just to be sure your answers agree with mine) and print a reference to it, immediately preceded by the letter X and immediately followed by the letter Z.

+   g) What command line did you use, and what was the output?

Answer:Your interaction should have looked something like the following:
unset y ; print X${y}Z
XZ

At this point, the "nothing" between the X and the Z should look familiar to you. The braces were needed around the variable name so the shell wouldn't try to print the value of a variable name y.

Now assign the value 123 to y and print a reference to y, surrounded by the characters X and Z again.

+   h) What command line did you use, and what was the output?

Answer:Your interaction should look like the following:
y=123 : print X${y}Z
X123

This step is just verifying that things are progressing as expected. You already did this sort of thing earlier.