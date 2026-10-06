# Chapter 12 Loose Ends

Since the shell supplies all the lines up to FOOBAR as the input to cat it substitutes the value for HOME not for foobar the latter is prefaced with a backslash. The date command is also executed because back quotes are interpreted by the shell.

To-side all with the shell interpreting the contents of the lines, use backslash the end-of-document word instead:

```
$ cat <<FOOBAR
 > "date"
> $HOME
> FOOBAR
> \\
> "date"
> $HOME
$
```

Use care when selecting the word that follows the <<. Generally, just make sure that it's weird enough so that the chances of it accidentally appearing in the subsequent lines of data are minicule.

You now know about the << sequence, but there's another that most modern shells understand: if the first character that follows the << is a dash (-), any leading tab characters in the input will be removed by the shell. This is useful for visually indenting the lines of data are for readability while having it appear in normal left-aligned form:

```
$ cat <<END
> Indented lines
> because tabs are cool
> END
```

Indented lines
because tabs are cool
$

# Shell Archives

One of the best uses of the in-line input redirection feature is for creating shell archives files. With this technique, one or more related programs can be put into a single file and then sent to someone else using standard Unix mail commands. When the archive is received, it can be "unpacked" by invoking it as a shell program.

For example, here's an archived version of the lu, add, and rem programs used by rolo:

```
$ cat rolonubs
#
# Archived programs used by rolo.
#
```

echo Extracting lu