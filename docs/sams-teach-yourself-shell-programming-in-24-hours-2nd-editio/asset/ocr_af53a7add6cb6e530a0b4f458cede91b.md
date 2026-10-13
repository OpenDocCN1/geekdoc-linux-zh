The execution of this script proceeds as follows:

+   1. The script executes reverse "$@" (effectively it calls reverse a b c).
+   2. The function reverse determines whether $# (the number of arguments) is greater than 0. In this case, $# will be equal to 3 (a b c).
+   3. Because $# is greater than 0, reverse saves the first argument, $1 (in this case a) in the local variable $arg, and then calls shift to remove it from $0. Now, $0 holds two arguments, b c.
+   4. The function reverse calls itself with the shortened $0.
+   5. The function reverse determines whether $# (the number of arguments) is greater than 0. In this case, $# will be equal to 2 (b c).
+   6. Because $# is greater than 0, reverse saves the first argument, $1 (in this case b) in the local variable $arg, and then calls shift to remove it from $0. Now, $0 holds just one argument, c.
+   7. The function reverse calls itself with the shortened $0.
+   8. The function reverse determines whether $# (the number of arguments) is greater than 0. In this case, $# will be equal to 1.
+   9. Because $# is greater than 0, reverse saves the first argument, $1 (in this case c) in the local variable $arg, and then calls shift to remove it from $0. Now, $0 holds no arguments.
+   10. The function reverse calls itself with the shortened $0.
+   11. The function reverse determines whether $# (the number of arguments) is greater than 0. Because there are no arguments in $0, this check fails and the function returns.
+   12. After the call to reverse returns, you output the value of the local variable $arg, in this case c, and return.
+   13. After the call to reverse returns, you output the value of the local variable $arg, in this case b, and return.
+   14. After the call to reverse returns, you output the value of the local variable $arg, in this case a, and return.

# Divide and Conquer

Recursion is normally used to solve problems using a technique known as divide and conquer. Basically, divide and conquer means that a problem is divided into smaller and smaller instances until an instance that is small enough to solve directly is found. Each instance that is too big to solve directly is solved recursively, and the solutions are combined to produce a solution to the original problem.