+   Listing 28-2B
+   Pascal code for the recip.p program.

```
{ Compute reciprocals }
program reciprocal(input, output);
var n, recip: integer;
begin
writeln('This program computes reciprocals.');
write('Enter a number: '); 
readln(n);
recip := 1 div n;
writeln('The reciprocal of ', n, ' is ', recip)
end.
```

This program introduces a few features that were not in the previous program:

+   *   `{ Compute reciprocals }`
+   An alternative way to write comments is to surround the comment with braces `{...}`.

+   *   `var n, recip: integer;`
+   This is a **declaration**. It tells the compiler to create two variables (var) to hold integers and to give them the names `n` and `recip`. Pascal requires that you declare all variables before you use them. A semicolon is placed at the end of this line to separate it from those that follow.

+   *   `write('Enter a number: ');`
+   `write` is a standard Pascal procedure, used to write output on the standard output. Unlike `writeln`, `write` does not start a new line after it finishes printing.

+   *   `readln(n);`
+   This `readln` statement obtains the user’s input from the standard input and stores it in the variable `n`.

+   *   `recip := 1 div n;`
+   This line computes the reciprocal. The computer first divides the integer `1` by the contents of the variable `n`, then assigns the result to the variable `recip`. In Pascal, `div` is used for dividing two integers. The pair of symbols `:=` is treated as one operator, called the *assignment operator*. It assigns the value of the expression `1 div n` to the variable `recip`.

+   *   `writeln('The reciprocal of ', n, ' is ', recip)`
+   This is a `writeln` with four arguments. It will print out the string `"The reciprocal of "`, followed by the value of the variable `n`, the string `" is "`, and finally the value of the variable `recip`.