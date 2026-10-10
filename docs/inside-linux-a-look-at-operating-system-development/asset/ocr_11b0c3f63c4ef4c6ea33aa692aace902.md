strings. This conflicts with the ability to group several options together, but that is a price well worth paying for the sake of consistency.

All Linux commands are invoked indirectly (through run-time library functions) or directly by calling the C function

```
int execve (const char \*filename,   const char \*argv [],   const char \*envp []);
```

The commands are integer valued functions taking three arguments

```
int main (int argc, char \*argv[], char \*envp[]);
```

The call can be from within a shell, in which case the user only sees the command name and a list of arguments. Likewise, the command can be a shell script, in which case the argument list and environment are converted into named variables which can be manipulated as described in Substitution of variables on page 44 and used in expressions as described in Selection and Iteration on pages 47 and 49. The important point is that every process starts with these two arrays of pointers to strings.

# Environment variables

The environment variables are structured as a set of name-value pairs. The library function getenv can be used to search the set for the value of a specified name. It will return a pointer to the value (which may be an empty string), or NULL if it is not defined. Shell scripts can easily determine if a name is defined, and if so, what its value is.

# Standard input

User programs can also read commands from the user's keyboard (or other redirected source).

Normally the keyboard input is pre-processed within the kernel so that the user program doesn't have to bother figuring out how to delete characters or words, how to echo characters, how escape characters work, etc. This is called *cooked* mode.