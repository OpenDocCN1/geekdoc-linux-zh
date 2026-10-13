# OPTIONS

+   - `--all, -a`—Print all matching executables in `PATH`, not just the first.
+   - `--read-alias, -i`—Read aliases from stdin, reporting matching ones on stdout. This is useful in combination with using an alias for which itself. For example `alias which='alias | which -i`.
+   - `--skip-alias`—Ignore option `--read-alias`, if any. This is useful to explicate search for normal binaries, while using the `--read-alias` option in an alias for which.
+   - `--skip-dot`—Skip directories in `PATH` that start with a dot.
+   - `--skip-tilde`—Skip directories in `PATH` that start with a tilde and executables which reside in the `HOME` directory.
+   - `--show-dot`—If a directory in `PATH` starts with a dot and a matching executable was found for that path, then print `/programname` rather than the full path.
+   - `--show-tilde`—Output a tilde when a directory matches the `HOME` directory. This option is ignored when which is invoked as root.
+   - `--tty-only`—Stop processing options on the right if not on tty.
+   - `--version, -v, -V`—Print version information on standard output then exit successfully.

# RETURN VALUE

which returns the number of failed arguments, or -1 when no program name was given.

# EXAMPLE

A useful way to use this utility is by adding an alias to which like the following:

```
alias which='which --tty-only --show-tilde --show-dot'
```

This will print the readable ~/ and ./ when starting which from your prompt while still printing the full path when used from a script:

```
> which q2 ~/bin/q2 > echo 'which q2' /home/carlo/bin/q2
```

Aliases are also supported, through the use of an alias for which. An example alias for which that is using this feature is as follows:

```
alias which='alias | which --tty-only --read-alias --show-tilde --show-dot'
```

This will print the output of an alias for each alias that matches one of the given arguments; for example, using this alias on itself in a tcsh:

```
$ alias which alias | /usr/bin/which -i !\^ $ which which which
→ alias | ./which -i !* /usr/bin/which
```

# BUGS

The HOME directory is determined by looking for the HOME environment variable, which aborts when this variable doesn’t exist. This will consider two equivalent directories to be different when one of them contains a path with a symbolic link.