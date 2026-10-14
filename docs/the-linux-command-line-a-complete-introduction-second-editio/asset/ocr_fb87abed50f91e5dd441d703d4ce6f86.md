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

# User-Defined Actions