Creating an associative array is also slightly different in the zsh shell. You must first declare it using the `typeset` command:

```
$ typeset -A test $
```

Once you’ve declared the variable as being an associative array, you can define keys and values. This is where things are a little different. In the zsh shell, you just alternate listing the keys and values:

```
variable=( key1 value1 key2 value2 . . . )
```

Thus, to add data to the `test` array, do this:

```
$ test=( fruit banana vegetable carrot age 18 )
$ echo ${test[fruit]}
banana
$ echo ${test[age]}
18
$
```

Because of this syntax, every key must be assigned a value in the zsh associative array.

# # Built-in commands

The zsh shell is unique in that it allows you to expand the built-in commands available in the shell. This provides for a wealth of speedy utilities at your fingertips for a host of different applications.

This section describes the core built-in commands, along with the various modules available at the time of this writing.

# ## Core built-in commands

The core of the zsh shell contains the basic built-in commands you’re used to seeing in other shells. Table 23.4 describes these built-in commands.

**TABLE 23.4 The zsh Core Built-In Commands**

| Command | Description | 
|---|---| 
| alias | Defines an alternate name for a command and arguments. |
| autoload | Preloads a shell function into memory for quicker access. |
| bg | Executes a job in background mode. |
| bindkey | Binds keyboard combinations to commands. |
| builtin | Executes the specified built-in command instead of an executable file of the same name. |
| bye | The same as exit. |

*Continued*