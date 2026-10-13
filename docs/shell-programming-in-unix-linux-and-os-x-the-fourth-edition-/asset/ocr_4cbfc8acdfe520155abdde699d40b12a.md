![](bbox=[0.143, 0.116, 0.757, 0.167])

Figure 5.6  `echo "$address"`

Where this gets a bit weird is that double quotes can be used to hide single quotes from the shell, and vice versa:

```
```sh
$ x="' Hello,' he said"
$ echo $x
'Hello,' he said
$ article= 'Keeping the Logins from Lagging,' Bell Labs Record'
$ echo $article
'Keeping the Logins from Lagging,' Bell Labs Record
$
```
```

# The Backslash

Functionally, the backslash (used as a prefix) is equivalent to placing single quotes around a single character, though with a few minor exceptions. The backslash *escapes* the character that immediately follows it. The general format is

```
```sh
\c
```
```

where *c* is the character you want to quote. Any special meaning normally attached to that character is removed. Here is an example:

```
```sh
$ echo >
syntax error: 'newline or ;' unexpected
$ echo \>
>
$
```
```

In the first usage, the shell sees the `>` and thinks that you want to redirect echo’s output to a file, so it expects a filename to follow. Because it doesn’t, the shell issues the error message.

In the next usage, the backslash escapes the special meaning of the `>`, so it is passed along to echo as a character to be displayed.

```
```sh
$ x=*
$ echo \$x
$x
$
```
```

In this case, the shell ignores the `$` that follows the backslash, and as a result, variable substitution is not performed.