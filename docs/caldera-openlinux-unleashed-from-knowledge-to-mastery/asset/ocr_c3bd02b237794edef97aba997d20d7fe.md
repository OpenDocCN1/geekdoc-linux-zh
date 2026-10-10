objects in one embedded block and still be able to access them in any other blocks that follow. In other words, we can do the following:

```
blah blah blah
blah blah blah
blah blah blah
blah blah blah
<1--code
mycomment="They would have peace in Israel if you weren’t such a snotsle!"

-->
blah blah blah
blah blah blah
blah blah blah
blah blah blah
<1--code
print mycomment
-->
```

Although not necessary in this example, this functionality can be very useful when dealing with strings that may take a significant time to generate, such as a database query.

# ## Other Ways to Execute Code Dynamically

Python also provides the built-in function that will immediately execute commands that exist in a specified file. Just like exec(), it allows you to specify an optional global and local namespace after the initial filename argument.

Python also has an eval() function that will return the result of an expression passed to it as a string.

```
eval(expression[,globals[,locals]])
```

These functions are very powerful because they allow you to dynamically create and evaluate Python code, without launching a separate interpreter.

To finish our function, we simply print any lines exactly as they appear if they are not part of a code block.

The last few lines that appear outside our function definition parse the command-line arguments passed to the script and output any necessary informational messages. To access the arguments passed to our script, we use the object sys.argv, which consists of a list of arguments. The first (zero) element of the list is the name of the script itself,