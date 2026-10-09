# **`set +o`**: `TURNS` SHELL FEATURES `ON` AND `OFF`

The `set` builtin, when used with the `-o` or `+o` option, enables, disables, and lists certain `bash` features. For example, the following command turns on the `noclobber` feature (page 156):

```
$ set -o noclobber
```

You can turn this feature off (the default) by giving this command:

```
$ set +o noclobber
```

The command `set -o` without an option lists each of the features controlled by `set`, followed by its state (on or off). The command `set +o` without an option lists the same features in a form you can use as input to the shell. Table 9-13 lists `bash` features. This table does not list the `-i` option because you cannot set it. The shell sets this option when it is invoked as an interactive shell. See page 1024 for a discussion of other uses of `set`.

# **`shopt`**: `TURNS` SHELL FEATURES `ON` AND `OFF`

The `shopt` (shell option) builtin enables, disables, and lists certain `bash` features that control the behavior of the shell. For example, the following command causes `bash` to include filenames that begin with a period (.) when it expands ambiguous file references (the `-s` stands for `set`):

```
$ shopt -s dotglob
```

You can turn this feature off (the default) by giving the following command (the `-u` stands for `unset`):

```
$ shopt -u dotglob
```

The shell displays how a feature is set if you give the name of the feature as the only argument to `shopt`:

```
$ shopt dotglob
          dotglob off
```

Without any options or arguments, `shopt` lists the features it controls and their states. The command `shopt -s` without an argument lists the features controlled by `shopt` that are set or on. The command `shopt -u` lists the features that are unset or off. Table 9-13 lists `bash` features.

# Setting `set +o` features using `shopt`

> **tip** You can use `shopt` to set/unset features that are otherwise controlled by `set +o`. Use the regular `shopt` syntax using `-s` or `-u` and include the `-o` option. For example, the following command turns on the `noclobber` feature:

```
$ shopt -o -s noclobber
```