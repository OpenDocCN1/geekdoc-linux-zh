# Shell Scripting Basics

There is a limitation to the test numeric conditions though. Try this script:

```
$ cat test6
#!/bin/bash
# testing floating point numbers
vall=`echo "scale=4; 10 / 3 " | bc
echo The test value is $vall
if [ $vall -gt 3 ]
then
echo The result is larger than 3
fi
$ ./test6
The test value is 3.3333
./test6 line 5: [ : 3.3333: integer expression expected
$ 
```

This example uses the calculator to produce a floating-point value, stored in the vall variable. Next, it uses the test command to evaluate the value. Something obviously went wrong here.

In Chapter 8, you learned how the bash shell is handling floating-point values; there's still a problem in this script. The test command wasn't able to handle the floating-point value that was stored in the vall variable.

Remember, the only numbers the bash shell can handle integers. When we utilize the bash calculator, we just fool the shell into storing a floating-point value in a variable as a string value. This works perfectly fine if all you need to do is display the result, using an echo statement, but this doesn't work in numeric-oriented functions, such as our numeric test condition. The bottom line is that you're not able to use integer values in the test command.

# String comparisons

The test command also allows you to perform comparisons on string values. Performing comparisons on strings can get tricky, as you'll see. Table 9-2 shows the comparison functions you can use to evaluate two string values.

The following sections describe the different string comparisons available.

# String equality

The equal and not equal conditions are fairly self-explanatory with strings. It's pretty easy to know when two string values are the same or not:

```
$ cat test7
#!/bin/bash
```