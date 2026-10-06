# Part IV Alternative Linux Shells

# Discipline functions

A ksh93 shell feature related to command redirection is a discipline function. A discipline function is a function that operates on a variable. There are three basic discipline functions:

+   - get: To get the value of the function variable.
- set: To set the value of the function variable.
- unset: To reset the value of a function variable.

You define a discipline function similarly to how you would define a normal function (the ksh93 shell uses the function command, similar to how the bash shell does it). The key for a discipline function is how it returns the resulting value.

If you're using the discipline function for a variable, instead of using the return command, a discipline function uses the special .sh.value variable. This allows you to use the function just like a variable, as each time you retrieve the discipline function name, it returns the value stored in .sh.value variable.

Here's an example of defining and using a discipline function:

```
$ function date.get {
  .sh.value=$( date '+%A, %B d, %Y' )
}$
```

Now the date variable will return the formatted date any time you retrieve it:

```
$ echo date
Monday, January 14, 2008
$
```

You set the discipline function to automatically alter the way a variable is set in an assignment statement:

```
$ function sqrt.set {
  .sh.value=$( sqrt($.sh.value)))
}$
```

Whenever you assign a value to the sqrt variable, the discipline function automatically calculates the square root of the value and assigns the result to the variable:

```
$ sqrt=9
$ echo $sqrt
3
$ sqrt=16
$ echo $sqrt
4
n
```