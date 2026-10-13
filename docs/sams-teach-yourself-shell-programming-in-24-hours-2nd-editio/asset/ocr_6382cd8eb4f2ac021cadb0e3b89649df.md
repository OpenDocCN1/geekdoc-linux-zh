same function, you just copied the function from one script to the other. This method works fine when you are dealing with one or two scripts, but it breaks down with many scripts. Say you have a dozen scripts that share a function and you located a bug in that function. You can image how hard it would be to fix every one of those scripts. A repository or library of common functions would reduce the complexity of developing and maintaining these shell scripts.

# What Is a Library?

Creating a library of functions is exactly like creating a shell script. The only difference between a script and a library is that a library contains only function definitions, whereas a script can contain both function definitions and executable code. The executable code in a script consists of all the commands in the script outside of the function definitions.

In the following shell script, lines 1, 2, and 4 are executable code:

```
```sh
1 #!/bin/sh
2 MSG="hello"
3 echo_error() { echo "ERROR:" $9 t+42 ; }
4 echo_error $MSG
```
```

Line 3, which contains a function definition, is not executable code.

A library does not contain any executable code; it contains only function definitions. For example, the following is a library:

```
```sh
#!/bin/sh
echo_error() { echo "ERROR:" $9 t+42 ; }
echo_warning() { echo "WARNING:" $9 t+1:62 ; }
```
```

Strictly speaking, nothing prevents a library from containing executable code; the distinction between a script and a library is purely a conceptual one.

# Using a Library

You can access the functions defined as a library in your scripts using the . command. Its syntax is

. file

Here, file is the pathname to the library. When a library is accessed via the . command, it is referred to as sourced or loaded. If file is not a valid pathname or not a script, the shell will display an error message and then exit. For this reason, most scripts load all of their libraries before executing any commands.

For example, if the functions given in the previous example are stored in a file called messages.sh, the following command can be used to load them:

```
```sh
. messages.sh
```
```