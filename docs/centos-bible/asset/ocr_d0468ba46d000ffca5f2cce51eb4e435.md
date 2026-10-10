# Part III

# Administration

that follow would all store the value 64 in the result variable. The last command gets a random number between 0 and 10 and echoes the results back to you.

```
```text
BIGNUM=1024
let result=$bignum/16
result=`expr $bignum / 16`
result=`echo " $bignum / 16" | bc -l`
let foo=$random%10; echo $foo
```
```

> **NOTE** While most elements of shell scripts are relatively freeform (where white space, such as spaces or tabs, is insignificant), both `let` and `expr` are particular about spacing. The `let` command insists on no spaces between each operand and the mathematical operator, whereas the syntax of the `expr` command requires white space between each operand and its operator. In contrast to those, `bc` isn't picky about spaces but can be trickier to use because it does floating-point arithmetic.

To see a complete list of the kinds of arithmetic you can perform using the `let` command, type `help let` at the Bash prompt.

# Using Programming Constructs in Shell Scripts

One of the features that make shell scripts so powerful is their implementation of looping and conditional execution constructs is similar to those found in more complex scripting and programming languages. You can use several different types of loops, depending on your needs.

# The `if...then` Statements

The most commonly used programming construct is conditional execution, or the `if` statement. It is used to perform actions only under certain conditions. There are several variations, depending on whether you're testing one thing, or want to do one thing if a condition is true, but another thing if a condition is false, or if you want to test several things one after the other.

The first `if...then` example tests if VARIABLE is set to the number 1. If it is, then the `echo` command is used to say that it is set to 1. The `fi` then indicates that the `if` statement is complete, and processing can continue.

```
```text
VARIABLE=1
if [ $VARIABLE -eq 1 ]; then
echo "The variable is 1"
fi
```
```

Instead of using `-eq`, you can use the equals sign (=), as shown in the following example. The = is used for comparing string values, while -eq is used for comparing numbers.

Using the `else` statement, different words can be echoed if the criterion of the `if` statement isn't met ($STRING="friday"). Keep in mind that it's good practice to put strings in double quotes.