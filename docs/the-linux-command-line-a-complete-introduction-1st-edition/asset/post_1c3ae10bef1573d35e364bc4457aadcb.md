
## Table 17-4 (continued)

| Operator | Description |
|---|---|
| ( ) | Groups tests and operators together to form larger expressions. This is used to control the precedence of the logical evaluations. By default, find evaluates from left to right. It is often necessary to override the default evaluation order to obtain the desired result. Even if not needed, it is helpful sometimes to include the grouping characters to improve readability of the command. Note that since the parentheses characters have special meaning to the shell, they must be quoted when using them on the command line to allow them to be passed as arguments to find. Usually the backslash character is used to escape them. |

With this list of operators in hand, let’s deconstruct our find command. When viewed from the uppermost level, we see that our tests are arranged as two groupings separated by an -or operator:

```
(expression 1) -o (expression 2)
```

This makes sense, since we are searching for files with a certain set of permissions and for directories with a different set. If we are looking for both files and directories, why do we use -or instead of -and? Because as find scans through the files and directories, each one is evaluated to see if it matches the specified tests. We want to know if it is either a file with bad permissions or a directory with bad permissions. It can’t be both at the same time. So if we expand the grouped expressions, we can see it this way:

```
(file with bad perms) -o (directory with bad perms)
```

Our next challenge is how to test for "bad permissions." How do we do that? Actually we don’t. What we will test for is "not good permissions," since we know what "good permissions" are. In the case of files, we define good as 0600; for directories, 0700. The expression that will test files for "not good" permissions is:

```
-type f -and -not -perms 0600
```

and the expression for directories is:

```
-type d -and -not -perms 0700
```

As noted in Table 17-4, the -and operator can be safely removed, since it is implied by default. So if we put this all back together, we get our final command:

```
find ~ (-type f -not -perms 0600) -o (-type d -not -perms 0700)
```

However, since the parentheses have special meaning to the shell, we must escape them to prevent the shell from trying to interpret them. Preceding each one with a backslash character does the trick.

There is another feature of logical operators that is important to understand. Let’s say that we have two expressions separated by a logical operator:

expr1 -operator expr2

In all cases, expr1 will always be performed; however, the operator will determine if expr2 is performed. Table 17-5 shows how it works.

## Table 17-5: find AND/OR Logic

| Results of expr1 | Operator | expr2 is... |
|---|---|---|
| True | -and | Always performed |
| False | -and | Never performed |
| True | -or | Never performed |
| False | -or | Always performed |

Why does this happen? It’s done to improve performance. Take -and, for example. We know that the expression expr1 -and expr2 cannot be true if the result of expr1 is false, so there is no point in performing expr2. Likewise, if we have the expression expr1 -or expr2 and the result of expr1 is true, there is no point in performing expr2, as we already know that the expression expr1 -or expr2 is true.

Okay, so this helps things go faster. Why is this important? Because we can rely on this behavior to control how actions are performed, as we shall soon see.

## Actions

Let’s get some work done! Having a list of results from our find command is useful, but what we really want to do is act on the items on the list. Fortunately, find allows actions to be performed based on the search results.

## Predefined Actions

There are a set of predefined actions and several ways to apply user-defined actions. First let’s look at a few of the predefined actions in Table 17-6.

## Table 17-6: Predefined find Actions

| Action | Description |
|---|---|
| -delete | Delete the currently matching file. |
| -ls | Perform the equivalent of ls -dils on the matching file. Output is sent to standard output. |
| -print | Output the full pathname of the matching file to standard output. This is the default action if no other action is specified. |
