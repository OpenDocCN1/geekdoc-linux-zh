If read receives fewer than the expected number, the extra variables are empty, while an excessive amount of input results in the final variable containing all of the extra input.

If no variables are listed after the read command, a shell variable, REPLY, will be assigned all the input:

```
#!/bin/bash

# read-single: read multiple values into default variable
echo -n "Enter one or more values > "
read
echo "REPLY = '$REPLY'"
```

Running this script results in this:

```
[me@linuxbox ~]$ read-single
Enter one or more values > a b c d
REPLY = 'a b c d'
```

# Options

read supports the following options:

Table 28-1: read Options

| Option | Description |
|---|---|
| -a array | Assign the input to array, starting with index zero. We will cover arrays in Chapter 35. |
| -d delimiter | The first character in the string delimiter is used to indicate end of input, rather than a newline character. |
| -e | Use Readline to handle input. This permits input editing in the same manner as the command line. |
| -i string | Use string as a default reply if the user simply presses Enter. Requires the -e option. |
| -n num | Read num characters of input, rather than an entire line. |
| -p prompt | Display a prompt for input using the string prompt. |