```
grape
apricot
```

You will notice that banana is not printed out. This is because when the fruit variable contains the word banana, the continue command is executed and the program jumps up to the for keyword and continues the loop iteration with the next item in the list.

# The echo Command

The echo command does exactly what you would think it does. It takes anything passed to it and prints it out, essentially echoing your input.

Here is the syntax for the echo command:

```
echo [-neE] [arg...]
```

There are several parameters you can pass to echo that modify its behavior. These could be used to format the output, making it more readable to the operator. They are

+   - -n—Does not print a newline character at the end of output.
+   - -e—Turns on the interpretation of the backslash escape sequences.
+   - -E—Turns off the interpretation of the backslash escape sequences.

The following backslash escape sequences are recognized by the echo command:

+   - \a—Alert (usually sounds the bell)
+   - \b—Backspace
+   - \c—Suppresses any trailing newline characters
+   - \f—Form feed
+   - \n—New line
+   - \r—Carriage return
+   - \t—Horizontal tab
+   - \v—Vertical tab
+   - \\—Backslash
+   - \nnn—The character whose ASCII code is nnn (octal)

The value returned from echo is always 0, which is success.