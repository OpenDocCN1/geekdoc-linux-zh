If you use Listing 11.2, you need to type only three things: the script name with the desired username and the password (twice). For instance, if the script is called mkuser, you can use it like this:

```
# mkuser ajones
Changing password for user ajones
New password:
Retype password:
passwd: all authentication tokens updated successfully
```

Most of the script's programs operate silently unless they encounter problems, so the interaction (typing the passwords, which do not echo to the screen) is a result of just the passwd command. In effect, Listing 11.2's script replaces seven lines of commands with one. Every one of those lines uses the username, so by running this script, you also reduce the chance of a typo causing problems.

# Using Variables

Certification Objective

Another type of variable is assigned within scripts—for instance, variables can be set from the output of a command. These variables are also identified by leading dollar signs, but they are typically given names that at least begin with a letter, such as $Addr or $Name. (When values are assigned to variables, the dollar sign is omitted shortly.) You can then use these variables in conjunction with normal commands as if they were command parameters, but the value of the variable is passed to the command.

For instance, consider Listing 11.3, which checks to see if the computer's router is up-wise with the help of the ping utility. This script uses two variables. The first is $ip, which is extracted from the output of using grep, tr, and cut commands. When you're assigning a value to a variable from a command, which should be enclosed in back-tick characters (`), which appear on the same key as the tilde (~) on most keyboards, are not ordinary single quotes, which appear on the same key as the regular quote (") on most keyboards. The second variable, $ping, simply points to the ping program. It can just as easily be omitted, with subsequent uses of $ping replaced by the full path to the program or simply by relying on the $PATH environment variable to find the program). Variables like these are some times used to make it easier to modify the script in the future. For, if you move the ping program, you need to modify only one line of the script. Variables can also be used in conjunction with conditionals to ensure that the script works on more systems—for instance, if ping were called something else on some systems.

*