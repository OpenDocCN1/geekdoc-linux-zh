So what kind of conditions can we test for? If you're dealing with numbers, here are the conditional expressions you can use. In other words, any of these expressions can go inside the brackets on the if or elif statement:

num1 -eq num2	True if num1 equals num2.
num1 -ne num2	True if num1 is not equal to num2.
num1 -lt num2	True if num1 is less than num2.
num1 -gt num2	True if num1 is greater than num2.
num1 -le num2	True if num1 is less than or equal to num2.
num1 -ge num2	True if num1 is greater than or equal to num2.

If you're comparing character strings, these are the valid conditional expressions:

str1 = str2	True if str1 and str2 are identical.
str1 != str2	True if str1 and str2 are not identical.
-n str1	True if str1 is not null (length is greater than zero).
-z str1	True if str1 is null (length is zero).
You can also test certain file conditions, such as whether or not files exist, the type of file, and so on. Here are the conditional expressions for files:

-f somefile	True if somefile exists and is an ordinary file.
-d somefile	True if somefile exists and is a directory.
-s somefile	True if somefile contains data (the size is not zero).
-r somefile	True if somefile is readable.
-w somefile	True if somefile is writable.
-x somefile	True if somefile is executable.

And finally, here are the logical operators, for performing tests that involve and, or, and not conditions.

cond1 -a cond2	True if both cond1 and cond2 are true.
cond1 -o cond2	True if either cond1 or cond2 is true.
! cond1	True if cond1 is false.