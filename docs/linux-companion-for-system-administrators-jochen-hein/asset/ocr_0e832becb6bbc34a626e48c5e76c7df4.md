# THE SHELL AS A CONNECTING LINK BETWEEN VARIOUS PROGRAMS 307

The characters << followed by an arbitrary character instruct the shell to use up to the next occurrence of this character sequence as the standard input. Shell variables are expanded, other special characters are not.

```
cat << EOF
The text is to be output.
It can be of (almost) arbitrary length.
nThe script was started by user '$USER'.
EOF
```

Listing 10.56 An example of a 'here' document.

# 8.8.2 Expanding special characters

The shell uses a series of characters that have a special meaning in the input or in shell scripts. The fact that the shell considers nearly everything as a string, which also applies to commands entered by the user and to shell scripts. Any of these strings are first searched for special characters, which are processed before the shell subsequently executes the required command.

The process of how the commands to be executed are generated from the input, and when specific substitutions are to be made, is standardized. The POSIX standard describes the process that has developed over time together with the sh. Thus, some decisions have been established although now these would no longer be made in the same way.

# File name expansion

When entering a command, you can either enter the file name(s) manually or use the file name expansion mechanism of the shell. Quite often one wants to process a group of files together, and this group is often identified by a common element in the file names. This is where you would normally use the shell's file name expansion.

Various special characters (wildcards) can be used for this functionality. First of all, an asterisk (*) stands for an arbitrary number of characters in a file name. As opposed to DOS, * stands for (nearly) all files, except those names begin with a dot (.). The question mark (?) stands for exactly one character in a file name. As opposed to DOS, the asterisk can appear at any position in the pattern, not just at the end. Except for the specific use mentioned above, the dot (.) has no special meaning under UNIX.

These expansions are carried out by the shell. Thus, when you enter ls *.c at the shell prompt, the ls command already contains a list of C files as parameter. In cases of emergency, for example, if no ls is present on an