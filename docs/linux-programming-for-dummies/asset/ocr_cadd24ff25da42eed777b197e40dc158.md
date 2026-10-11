```
mailprogam "Good News" memo1
```

The following steps describe what happens as the program runs:

+   1. Linux runs the bash shell (#!/bin/bash).
+   2. Linux substitutes Good News for $1 in the program and substitutes memo1 for $2.
+   3. The mail utility uses the default destination address bob@mycomputer to send the e-mail.

# Overriding default values

You can override default values by writing logic into your program to determine the number of arguments that are passing on the command line.

I decide, for example, that two arguments are to pass to the program whenever I want to use the default destination addresses, and three arguments are to pass if I want to override the default destination addresses. Suppose that your program contains a destination address that you use for every e-mail that you send by using your program. You can override the destination address by passing a new destination address from the command line whenever your call your program. Linux then uses the new destination address instead of the designation address written inside your program.

You must modify the e-mail program to determine whether two or three arguments are passing as you call the program. Basing its decision on the number of arguments, the program then executes one set of instructions or another set of instructions.

You must make the following three changes to the program:

+   ✔ Determine the number of arguments on the command line.
+   ✔ Determine which instructions to execute depending on the number of arguments.
+   ✔ Insert two sets of instructions to handle two arguments and three arguments.

The $# variable contains the number of arguments that pass to the command line. You can use the $# as the number of argument itself.

You use the if statement to compare the value of $# with the number of arguments that’s necessary to run each set of instructions. (See Chapter 7 for