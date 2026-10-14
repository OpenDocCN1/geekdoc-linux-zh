
| Results of expr1 | Operator | expr2 is ... |
|---|---|---|
| True | -and | Always performed |
| False | -and | Never performed |
| True | -or | Never performed |
| False | -or | Always performed |

Why does this happen? It’s done to improve performance. Take -and, for example. We know that the expression expr1 -and expr2 cannot be true if the result of expr1 is false, so there is no point in performing expr2. Likewise, if we have the expression expr1 -or expr2 and the result of expr1 is true, there is no point in performing expr2, as we already know that the expression expr1 -or expr2 is true.

OK, so it helps it go faster. Why is this important? It’s important because we can rely on this behavior to control how actions are performed, as we will soon see.

## Predefined Actions

Let’s get some work done! Having a list of results from our find command is useful, but what we really want to do is act on the items on the list. Fortunately, find allows actions to be performed based on the search results. There are a set of predefined actions and several ways to apply user-defined actions. First, let’s look at a few of the predefined actions listed in Table 17-6.

Table 17-6: Predefined find Actions

| Action | Description |
|---|---|
| -delete | Delete the currently matching file. |
| -ls | Perform the equivalent of ls -dTls on the matching file. Output is sent to standard output. |
| -print | Output the full pathname of the matching file to standard output. This is the default action if no other action is specified. |
| -quit | Quit once a match has been made. |

As with the tests, there are many more actions. See the find man page for full details.

In the first example, we did this:

```
find ~
```

This produced a list of every file and subdirectory contained within our home directory. It produced a list because the -print action is implied if no other action is specified. Thus, our command could also be expressed as follows:

```
find ~ -print
```

We can use find to delete files that meet certain criteria. For example, to delete files that have the file extension .bak (which is often used to designate backup files), we could use this command:

```
find ~ -type f -name '*.bak' -delete
```

In this example, every file in the user's home directory (and its subdirectories) is searched for filenames ending in .bak. When they are found, they are deleted.

> **WARNING**
> It should go without saying that you should use extreme caution when using the -delete action. Always test the command first by substituting the -print action for -delete to confirm the search results.

Before we go on, let's take another look at how the logical operators affect actions. Consider the following command:

```
find ~ -type f -name '*.bak' -print
```

As we have seen, this command will look for every regular file (`-type f`) whose name ends with `.bak` (`-name '*.bak'`) and will output the relative pathname of each matching file to standard output (`-print`). However, the reason the command performs the way it does is determined by the logical relationships between each of the tests and actions. Remember, there is, by default, an implied `-and` relationship between each test and action. We could also express the command this way to make the logical relationships easier to see:

```
find ~ -type f -and -name '*.bak' -and -print
```

With our command fully expressed, let’s look at how the logical operators affect its execution:

| Test/Action | Is performed only if... |
|---|---|
| `-print` | `-type f` and `-name '*.bak'` are true |
| `-name '*.bak'` | `-type f` is true |
| `-type f` | Is always performed, since it is the first test/action in an `-and` relationship. |

Because the logical relationship between the tests and actions determines which of them are performed, we can see that the order of the tests and actions is important. For instance, if we were to reorder the tests and actions so that the `-print` action was the first one, the command would behave much differently.

```
find ~ -print -and -type f -and -name '*.bak'
```

This version of the command will print each file (the `-print` action always evaluates to true) and then test for file type and the specified file extension.

## User-Defined Actions
