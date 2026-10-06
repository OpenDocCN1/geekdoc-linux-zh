```
me@linux share $ cd bin
me@linux bin $ pwd
/usr/local/bin
```

Pathnames can be abbreviated as long as they are unambiguous. If we type:

```
me@linux ~ $ ls /usr/share<tab>
```

zsh will expand it into:

```
me@linux ~ $ ls /usr/local/share/
```

That can save a lot of typing! Arguments are provided for many commands. To invoke this feature, we type the command and the leading dash for an option, then hit the key:

```
me@linux ~ $ rm <-tab>
--force ignore nonexistent files, never prompt
--help display help message and exit
-i prompt before removal
-i prompt when removing many files
--interactive prompt under condition (defaulting to always)
--preserve-root do not treat / specially
--one-file-system stay within file systems of given as arguments
--preserve-root do not remove / (default)
--recursive -R r remove directories and their contents recursively
--verbose explain what is being done
--v output version information and exit
```

This displays a list of options for the command, and like the cd command, repeatedly pressing tab zsh to cycle through the options.

# Pathname Expansion

The shell provides several powerful additions to pathname expansion that can save steps when specifying file command arguments.
We can use "** to cause recursive expansion. For example, if we wanted to list every file ending with .txt in our home directory and subdirectories, we would have to do this in bash:

```
me@linux $ find -name "*.txt" | sort
```

In zsh, we could do this:

```
me@linux ~ $ ls *//*.txt
```

and get the same result.
And if that were not cool enough, we can also add qualifiers to the wildcard to perform many of the tests with the find command. For example:

```
me@linux ~ $ **/*.txt(@)
```