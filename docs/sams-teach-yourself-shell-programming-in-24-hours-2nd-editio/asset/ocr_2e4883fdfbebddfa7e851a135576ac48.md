# Quoting Ignores Word Boundaries

In English, you are used to quoting whole words or sentences. In shell programming, the special characters must be quoted, but it does not matter whether the regular characters are quoted in the same word, as follows:

```
$ echo 'Hello; world'
Hello; world
```

You can move the quotes off word boundaries as long as any special characters remain quoted. This command produces the same output as the preceding one:

```
$ echo 'Hel'lo'; 'w'or'ld
Hello; world
```

Of course, it is easier to read the line if the quotes are on word boundaries. This simple example illustrates the manner in which quoting can be used. Quoting off of word boundaries will be useful in some of the more complex quoting situations you will encounter.

# Combining Quoting in Commands

You can freely switch from one type of quoting to another within the same command. For example, the following command contains single quotes, a backslash, and double quotes:

```
$ echo The 'USER' variable contains this value > "|$USER|"
The 'USER' variable contains this value > |ranga|
```

As you can see from the output, you can intermixed multiple forms of quoting in the same command.

# Embedding Spaces in a Single Argument

To the shell, one or more spaces or tabs form a single command-line argument separator. For example, the output from the following command:

```
$ echo Name Address
```