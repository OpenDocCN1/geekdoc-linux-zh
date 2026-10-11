# ## ls

You can also add comments as multiple lines to your shell script. You can do so by placing your comments between `:’` and `‘`.

Consider the example below.

```
```
#!/bin/bash
:’
  This script calculates
  the square of 5.
‘
((area=5*5))
echo $area
```
```

So the string between `:’` and `‘` that is this script calculates the square of 5 is commented out from the script.

# ## Shell Variables

Variables in any programming language are used to store data in the form of characters and numbers. Shell scripts also support variables that store data that can be accessed by the Linux shell.

For instance, the simple example below shows a variable that stores some data and then prints it.

```
```
variable ="Hello"
echo $variable
```
```

Let us look at another example of a shell script that uses variables.

```
```
#!/bin/sh
echo "what is your name?"
read name
```
```