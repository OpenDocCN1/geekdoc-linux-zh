using similar syntax as would be used to invoke the subcommands themselves. For example, the command:

```
```
man -aw git diff
```
```

displays the manual page:

```
```
/usr/share/man/man1/git-diff.1.gz
```
```

To disable this behavior, use the `--no-subpages` option.

For example:

```
```
man -aw --no-subpages git diff
```
```

Will instead show the manual pages for both `git` and `diff`:

```
```
/usr/share/man/man1/git.1.gz
/usr/share/man/man3/Git.3pm.gz
/usr/share/man/man1/diff.1.gz
```
```

# ## Controlling Formatted Output

| Option | Description |
| :--- | :--- |
| `-P pager`, `--pager=pager` | Specify which output pager to use. By default, man uses `pager -s`. This option overrides the `SMANPAGER` environment variable, which in turn overrides the `PAGER` environment variable. It is not used in conjunction with `-f` or `-k`.<br><br>The value may be a simple command name or a command with arguments, and may use shell quoting (backslashes, single quotes, or double quotes). It may not use pipes to connect multiple commands; if you need that, use a wrapper script, which may take the file to display either as an argument or on standard input. |
| `-r prompt`, `--prompt=prompt` | If a recent version of `less` is used as the pager, man will attempt to set its prompt and |