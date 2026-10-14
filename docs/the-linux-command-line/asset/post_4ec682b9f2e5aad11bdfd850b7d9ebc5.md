
The script evaluates the file assigned to the constant FILE and displays its results as the evaluation is performed. There are two interesting things to note about this script. First, notice how the parameter $FILE is quoted within the expressions. This is not required, but is a defense against the parameter being empty. If the parameter expansion of $FILE were to result in an empty value, it would cause an error (the operators would be interpreted as non-null strings rather than operators). Using the quotes around the parameter insures that the operator is always followed by a string, even if the string is empty. Second, notice the presence of the exit commands near the end of the script. The exit command accepts a single, optional argument, which becomes the script's exit status. When no argument is passed, the exit status defaults to zero. Using exit in this way allows the script to indicate failure if $FILE expands to the name of a nonexistent file. The exit command appearing on the last line of the script is there as a formality. When a script “runs off the end” (reaches end of file), it terminates with an exit status of zero by default, anyway.

Similarly, shell functions can return an exit status by including an integer argument to the return command. If we were to convert the script above to a shell function to include it in a larger program, we could replace the exit commands with return statements and get the desired behavior:

```
test_file () {
    # test-file: Evaluate the status of a file
    
    FILE=~/.bashrc
    
    if [ -e "$FILE" ]; then
        if [ -f "$FILE" ]; then
            echo "$FILE is a regular file."
        fi
        if [ -d "$FILE" ]; then
            echo "$FILE is a directory."
        fi
        if [ -r "$FILE" ]; then
            echo "$FILE is readable."
        fi
        if [ -w "$FILE" ]; then
            echo "$FILE is writable."
        fi
        if [ -x "$FILE" ]; then
            echo "$FILE is executable/searchable."
        fi
    else
        echo "$FILE does not exist"
        return 1
    
}
fi
}
```

## String Expressions

The following expressions are used to evaluate strings:

Table 28-2: test String Expressions

| Expression | Is True If... |
|---|---|
| *string* | *string* is not null. |
| -n *string* | The length of *string* is greater than zero. |
| -z *string* | The length of *string* is zero. |
| *string1 = string2* <br> *string1 == string2* | *string1* and *string2* are equal. Single or double equal signs may be used, but the use of double equal signs is greatly preferred. |
| *string1 != string2* | *string1* and *string2* are not equal. |
| *string1 > string2* | *string1* sorts after *string2*. |
| *string1 < string2* | *string1* sorts before *string2*. |

**Warning:** the > and < expression operators must be quoted (or escaped with a backslash) when used with `test`. If they are not, they will be interpreted by the shell as redirection operators, with potentially destructive results. Also note that while the `bash` documentation states that the sorting order conforms to the collation order of the current locale, it does not. ASCII (POSIX) order is used in versions of `bash` up to and including 4.0.

Here is a script that incorporates string expressions:

```
#!/bin/bash

# test-string: evaluate the value of a string

ANSWER=maybe

if [ -z "$ANSWER" ]; then
echo "There is no answer." >&2
exit 1
fi
if [ "$ANSWER" = "yes" ]; then
    echo "The answer is YES."
elif [ "$ANSWER" = "no" ]; then
    echo "The answer is NO."
elif [ "$ANSWER" = "maybe" ]; then
    echo "The answer is MAYBE."
else
    echo "The answer is UNKNOWN."
fi
```

In this script, we evaluate the constant ANSWER. We first determine if the string is empty. If it is, we terminate the script and set the exit status to one. Notice the redirection that is applied to the echo command. This redirects the error message “There is no answer.” to standard error, which is the “proper” thing to do with error messages. If the string is not empty, we evaluate the value of the string to see if it is equal to either “yes,” “no,” or “maybe.” We do this by using elif, which is short for “else if.” By using elif, we are able to construct a more complex logical test.

## Integer Expressions

The following expressions are used with integers:

Table 28-3: test Integer Expressions

| Expression | Is True If... |
|---|---|
| integer1 -eq integer2 | integer1 is equal to integer2. |
| integer1 -ne integer2 | integer1 is not equal to integer2. |
| integer1 -le integer2 | integer1 is less than or equal to integer2. |
| integer1 -lt integer2 | integer1 is less than integer2. |
| integer1 -ge integer2 | integer1 is greater than or equal to integer2. |
| integer1 -gt integer2 | integer1 is greater than integer2. |

Here is a script that demonstrates them:

```
#!/bin/bash
```
