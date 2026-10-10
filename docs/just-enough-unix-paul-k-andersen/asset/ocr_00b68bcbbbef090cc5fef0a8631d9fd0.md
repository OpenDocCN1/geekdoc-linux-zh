# **STARTUP FILES**

# *20.8 User-Defined Variables*

# ## 20.8 User-Defined Variables

In addition to the standard shell variables, you can define your own variables. This is done by giving the variable a name and a value. Suppose, for example, that you were frequently using a long directory name such as `/usera/george/bin/stuff` and would prefer not to have to type it out each time. If you are using the `sh` or `ksh`, you could place the following line in your `.profile` to define a variable to hold the pathname:

```
```text
stuff=/usera/george/bin/stuff
```
```

Neither `sh` or `ksh` allows spaces around the equals sign.

This creates a variable named `stuff`, and gives it the pathname as a value. This variable will be known only to the login shell; if you also want it to be available to any subshells, you will have to "export" it:

```
```text
export stuff
```
```

(If you are a `ksh` user, you could also make `stuff` available to the subshells by defining it in the `.kshrc` file.)

`csh` handles user-defined variables somewhat differently. To create the variable `stuff` you could use the `set` command in your `.login` file:

`csh` allows spaces around the equals sign.

```
```text
set stuff = /usera/george/bin/stuff
```
```

This would define `stuff` for the login shell, but the definition would not carry over to any subshells. If you want your subshells to be able to use this variable, you have two choices. First, you could use the `setenv` command in your `.login` file:

Do not use an equals sign with `setenv`.

```
```text
setenv stuff /usera/george/bin/stuff
```
```

Or you could use the `set` command in your `.cshrc` file:

```
```text
set stuff = /usera/george/bin/stuff
```
```

Remember, any command in your `.cshrc` is run each time a new shell process is started, including subshells.

Having defined the variable `stuff` and given it a value, you can use it to save keystrokes. For example, you could list the files in the directory `/usera/george/bin/stuff` with the following command line:

```
```text
$ ls $stuff<Return>
```
```

Note the dollar sign preceding the variable name.

Traditionally, user-defined variable names are spelled in lowercase letters, to distinguish them from the standard shell variables.