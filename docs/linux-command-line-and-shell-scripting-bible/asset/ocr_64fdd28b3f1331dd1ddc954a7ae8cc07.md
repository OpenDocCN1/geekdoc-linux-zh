# Part III Advanced Shell Scripting

This time, since the function ended with an echo statement that completed successfully, the exit status of the function is 0, even though one of the commands in the function failed. The default exit status of a function can be a dangerous practice. Fortunately, there are a couple of other solutions for us.

# Using the return command

The bash shell uses the return command to exit a function with a specific exit status. The return command allows you to specify a single integer value to define the function exit status, providing an easy way for you to programmatically set the exit status of your function:

```
$ cat test5
#!/bin/bash
# using the return command in a function
```

```
function dbl {
  read -p "Enter a value: " value
  echo "doubling the value"
  return $value * 2
}
```

```
dbl
echo "The new value is $?"
$
```

The dbl function doubles the value contained in the $value variable provided by the user input. It then returns the result using the return command, which the script displays using the $ variable.

You must be careful when using this technique to return a value from a function. There are two things that can cause problems:

+   - Remember to retrieve the return value as soon as the function completes.
- Remember that an exit status can only be in the range of 0 to 255.

If you execute any other commands before retrieving the value of the function using the $? variable, the return value from the function will be lost (remember, the $? contains the exit status of the last executed command).

The second problem defines a limitation for using this return value technique. Since exit status must be less than 256, the result of your function must produce an integer value less than 256. Any values over that return an error value:

```
$ ./test5
Enter a value: 200
doubling the value
The new value is 1
$
```

You can't use this return value technique if you need to return larger integer values or a string value. Instead, you'll need to use another method, demonstrated in the next section.