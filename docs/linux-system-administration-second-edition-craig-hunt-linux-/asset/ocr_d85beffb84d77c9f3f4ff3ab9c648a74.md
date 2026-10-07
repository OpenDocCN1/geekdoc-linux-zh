prepackaged subroutines or other programs. Others include massive command sets that can do just about anything you might want. Sometimes it's difficult to tell the difference between a command and a prepackaged subroutine or outside program.

Shell scripting languages focus their command sets on file manipulations. Other scripting languages have other priorities. Perl, for instance, specializes in manipulating strings (collections of alphanumeric characters).

# ## The Bash Shell Scripting Language

Most Linux distributions make the Bash shell the default for all users. This shell provides the command-line prompt that's familiar to most Linux users. The Bash shell also provides a scripting language that allows users and administrators to automate repetitive tasks or even develop programs. This scripting language is well suited to automating repetitive tasks that you might ordinarily do at a command prompt. It can call other programs and utilities, so you can easily use common Linux utilities, such as grep and find, within a Bash script.

# ### Variables

Most variables in Bash scripts are strings—they hold alphanumeric sequences such as words or filenames. These variables are assigned via the equal sign, as in the following example:

```
```
IPCHAINS="/sbin/ipchains"
```
```

In this example, the string /sbin/ipchains is assigned to the variable $IPCHAINS. This variable can then be used to call the /sbin/ipchains program, to pass its name to other programs, or be manipulated in various ways. Assigning a variable in this way is very useful if you intend to change the variable's value. It's also sometimes used to make it easy to modify a script. For instance, if you move the ipchains program to /usr/sbin, you can change the variable assignment rather than many calls that use the $IPCHAINS variable.

To use a variable, you precede its name with a dollar sign ($). Thus, to call /sbin/ipchains, you could place the string $IPCHAINS on a line by itself (or followed by appropriate parameters for this utility). The only time you don't use the $ is when assigning a value to a variable. You can combine two or more variables by assigning them to a third, thus:

```
```
IPCHAINS="/sbin/ipchains"
OPTIONS="-A input -d 255.255.255.255 -j ACCEPT"
COMMAND="$IPCHAINS $OPTIONS"
```
```

The result of these three lines is a variable, COMMAND, that contains a complete ipchains command, including several options. You can use this ability to combine variables to provide greater flexibility. By combining variables in different ways based on the script's input (using conditionals and loops to guide the process), you can greatly expand the flexibility of a script.

Bash scripts can inherit certain variables from the user's work environment. These variables are therefore referred to as *environment variables*. These variables may be set by Bash scripts that are run automatically when a user logs in, and they typically contain information such as a list of directories to be searched for executable programs (PATH), the user's home directory (HOME), and many others, most of them used by specific programs. You can find out what environment variables are available to you by typing **env** at a Bash command prompt—but be aware that these variables