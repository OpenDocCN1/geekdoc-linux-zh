builtin controls one group of features, while the **shopt** builtin controls another group. You can also control many features from the command line you use to call **bash**.

# Features, options, variables?

> To avoid confusing terminology, this book refers to the various shell behaviors that you can control as *features*. The bash info page refers to them as “options” and “values of variables controlling optional shell behavior.”

# set ±-o: Turns Shell Features On and Off

The **set** builtin, when used with the -o or +o option, enables, disables, and lists certain **bash** features. For example, the following command turns on the **noclobber** feature (page 235):

```
$ set -o noclobber
```

You can turn this feature off (the default) by giving the command

```
$ set +o noclobber
```

The command **set -o** without an option lists each of the features controlled by **set** followed by its state (on or off). The command **set +o** without an option lists the same features in a form that you can use as input to the shell. Table 9-13 lists **bash** features.

# shopt: Turns Shell Features On and Off

The **shopt** (shell option) builtin enables, disables, and lists certain **bash** features that control the behavior of the shell. For example, the following command causes **bash** to include filenames that begin with a period (.) when it expands ambiguous file references (the -s stands for **set**):

```
$ shopt -s dotglob
```

You can turn this feature off (the default) by giving the command (the -u stands for **unset**)

```
$ shopt -u dotglob
```

The shell displays how a feature is set if you give the name of the feature as the only argument to **shopt**:

```
$ shopt dotglob
dotglob             off
```

The command **shopt** without any options or arguments lists the features controlled by **shopt** and their state. The command **shopt -s** without an argument lists the features controlled by **shopt** that are set or on. The command **shopt -u** lists the features that are unset or off. Table 9-13 (next page) lists **bash** features.

# Setting set +o features using shopt

> You can use **shopt** to set/unset features that are otherwise controlled by **set ±o**. Use the regular **shopt** syntax with -s or -u and include the -o option. For example, the following command turns on the **noclobber** feature:

```
$ shopt -o -s noclobber
```