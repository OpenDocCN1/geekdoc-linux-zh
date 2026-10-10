# Using the *return* command

The Bash shell uses the *return* command to exit a function with a specific exit status. The *return* command allows you to specify a single integer value to define the function exit status, providing an easy way for you to programmatically set the exit status of your function:

```
```
$ cat test5
#!/bin/bash
# using the return command in a function

function dbl {
    read -p "Enter a value: " value
    echo "doubling the value"
    return $[ $value * 2 ]
}

dbl
echo "The new value is $?"
$   
```
```

The `dbl` function doubles the integer value contained in the *$value* variable provided by the user input. It then returns the result using the *return* command, which the script displays using the *$?* variable.

You must be careful, however, when using this technique to return a value from a function. Keep the following two tips in mind to avoid problems:

+   - Remember to retrieve the return value as soon as the function completes.

+   - Remember that an exit status must be in the range of 0 to 255.

If you execute any other commands before retrieving the value of the function using the *$?* variable, the return value from the function is lost. Remember that the *$?* variable returns the exit status of the last executed command.

The second problem defines a limitation for using this return value technique. Because an exit status must be less than 256, the result of your function must produce an integer value less than 256. Any value over that returns an error value: