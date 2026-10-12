# ## Debugging assertions

When tracking down (debugging) errors in your code it is often useful to “comment-out” one or more lines of code by prefixing each line with the # hash character – as used for your comments. The Python interpreter will then omit execution of those lines so helps to localize where a problem lies. For example, where you suspect a variable assignment problem it can be excluded, like this:

![](bbox=[0.41, 0.32, 0.59, 0.45])

```
`# elem = elem / 2`
```

If the program now runs without errors, the commented-out assignment can be assumed to be problematic.

Another useful debugging technique employs the Python **assert** keyword to add error-checking code to your script. This examines a specified test expression for a Boolean True or False result, and reports an “AssertionError” when the test fails. Optionally, an assert statement can include a descriptive message to supply when reporting an AssertionError, and has this syntax:

*assert test-expression , descriptive-message*

When the test expression fails, the interpreter reports the AssertionError and halts execution of the script, but when the test succeeds, the assert statement does nothing, and execution of the script continues.

Employing assert statements is an effective way to document your script, as their descriptive messages provide commentary and their tests alert you when your code is erroneous.

# ### Assert versus Exception

At first glance, an AssertionError can appear confusingly similar to an Exception, but it is important to recognize their distinctions: