# Parameters and Variables

letters, digits, and underscores are often referred to as shell variables, or simply variables. A variable name must start with a letter or underscore, not with a number. Thus A76, MY_CAT, and __X__ are valid names, whereas 69TH_STREET (starts with a digit) and MY-NAME (contains a hyphen) are variables that you can name and assign values to user-created variables. One convention is to use uppercase letters for names of global variables (environment variables) and to use mixed-case or lowercase letters for other variables. You can change the values of user-created variables at any time, and you can make them readonly so that their value cannot be changed. You can also make user-created variables global. A global variable is available to all shells and other programs you fork from the original shell.

When you want to assign a value to a variable in the Bourne Again and Z Shells, use its name with no SPACES on either side of the equals sign:

```
$ myvar=abc
```

Refer to the beginning of Chapter 14 (page 681) if you are using them. When you want to use the value of a variable use its name preceded by a dollar sign ($):

```
$ echo myvar
```

Variables that have special meaning to the shell are called keyword shell variables (or simply keyword variables) and usually have short, mnemonic names. When you start a shell (by logging in, for example), the shell inherits its variables from the environment. Among these variables are HOME, which identifies your home directory, and PATH, which determines directories the shell searches and in what order to locate a command that you give the shell. The shell creates and initializes (with default values) other keyword variables when you start it; other variables do not exist until you set them.

You can change the values of most of the keyword shell variables at any time, although it is usually unnecessary to change the values of keyword variables initialized in /etc/profile. If you want to change the value of a variable, do so in one of the files in your home directory listed in the Interactive column of Table 12-1 on page 566. For more information see "Startup Files" on page 684. Just as you can make user-created variables global, you can make keyword variables this is often done automatically when the shell starts. You can also make a keyword variable readonly.

The names of one group of parameters do not resemble variable names. Most of these parameters have one-character names (for example, 1, ?, and #) and referenced (as are all variables) by preceding the name with a dollar sign (for example, $1, $?, and #). The values of these parameters reflect different aspects of your interaction with the shell. For example, whenever you give a command on the