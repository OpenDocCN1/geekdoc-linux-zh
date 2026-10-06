# Functions

A shell function is similar to a shell script, storing a series of commands for execution at a later time. However, because the shell stores a function in the computer's main memory (RAM) instead of a file on the disk, you can access it more quickly than you can access a script. Also, the shell preprocesses (parses) a function so that it starts up more quickly than a script. Finally, the shell executes a shell function in the same shell that called it.

You declare a shell function in your .bash_profile file, in the script that you use, or directly from the command line. The shell does not keep functions once you log out.

# Removing Variables and Functions

If you have a shell variable and a function with the same name, using unset removes the shell variable. If you then use unset with the same name, it removes the function.

The syntax that declares a shell function is

```
function-name ()
{
  commands
}
```

The function-name is the name you use to call the function. The commands comprise the list of commands the function executes when you call it. These commands can be anything you would include in a shell script, including calls to functions.

The next example shows how to create a simple function that displays the date, a header, and a list of the people who are using the system. This function runs the same commands as the whos script described on page 545:

```
$ whoson ()
{
  date
  echo "Users Currently Logged On"
  who
}
```