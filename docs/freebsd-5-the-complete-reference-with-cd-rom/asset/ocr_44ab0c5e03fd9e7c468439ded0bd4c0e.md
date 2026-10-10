# Displaying a Variable’s Value

Scripts must frequently display information. You can do so with the echo command. (This command is actually an external program, so passing a variable to echo is really the same thing as passing a variable to ls or any other external command.) Consider Listing 31-5, which is a template for experimenting with variables.

+   **Listing 31-5**
+   A Skeletal Variable Manipulation Script

```
#!/bin/sh
echo "The input variable is" $1
# Assign to a local variable
myvar=$1
# Perform some manipulation
# (To be filled in)
echo "The transformed variable is" $myvar
```

Suppose you call this script scatch. You might run it as follows:

```
$ ./scatch FreeBSD
The input variable is FreeBSD
The transformed variable is FreeBSD
```

The echo command echoes to the display any and all parameters it’s given. Thus, this command echoes both the information strings, such as The input variable is, and the value of the $1 variable. Because Listing 31-5 is a simple skeleton that doesn’t actually manipulate the variable in any way, that variable is unchanged.

# Setting a Variable to a User’s Input

So far, this chapter has shown extremely short scripts as examples. Scripts can be quite complex, though. Such complex scripts may ask a user for input—say, to prompt for a series of usernames or information that’s to be used in processing. Prompting for input in this way often creates a more user-friendly script than would result if the script required all its inputs as parameters. To obtain such input, you can use the read command, which accepts input from the user, who terminates input by pressing ENTER. For instance, consider Listing 31-6, which shows read in action.

+   **Listing 31-6**
+   A Script Demonstrating the Use of read

```
#!/bin/sh
echo "Please enter some information:"
read info
echo "You typed " $info
exit 0
```