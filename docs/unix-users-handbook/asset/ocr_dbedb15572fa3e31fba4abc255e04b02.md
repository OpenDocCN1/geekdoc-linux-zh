![](bbox=[0.03, 0.06, 0.13, 0.14])

the shell script’s positional parameters, because the **awk** variables are enclosed in single quotes and the shell ignores them.

But I don’t want to just talk about it. Let’s take a look at some examples.

This simple example lists just the terminals that are active on your system in which the terminal name is the second field of a **who** listing:

```
who | awk ' \{ print $2 \}'
```

Here is an example of running **who** and then running this one-line command:

```
marty p $ who
thomfsu  console       Feb 22 15:21   (:0)
marty p     pts/3     May 31 06:03 (atlm0216.atl.hp.com)
marty p $ who | awk '{print $2}'
console
pts/3
marty p $
```

![](bbox=[0.03, 0.55, 0.13, 0.63])

This output shows only the active terminals on the system.

Note that **cut** could have done this also, but you would have had to know exactly which columns the terminal name occupied in the **who** output, as shown below:

```
marty p $ who
thomfsu  console      Feb 22 15:21      (:0)
marty p      pts/3      May  31  06:03
(atlm0216.atl.hp.com)
marty p $ who | cut -c12-20
console
pts/3
marty p $
```

If the user or terminal name is longer than normal in any line, this command does not work. The **awk** example will work because it looks at fields, not columns.