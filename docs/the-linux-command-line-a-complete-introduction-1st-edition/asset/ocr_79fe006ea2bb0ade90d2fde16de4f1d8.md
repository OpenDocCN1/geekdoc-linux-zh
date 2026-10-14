There is another feature of logical operators that is important to understand. Let’s say that we have two expressions separated by a logical operator:

expr1 -operator expr2

In all cases, expr1 will always be performed; however, the operator will determine if expr2 is performed. Table 17-5 shows how it works.

# Table 17-5: find AND/OR Logic

| Results of expr1 | Operator | expr2 is... |
|---|---|---|
| True | -and | Always performed |
| False | -and | Never performed |
| True | -or | Never performed |
| False | -or | Always performed |

Why does this happen? It’s done to improve performance. Take -and, for example. We know that the expression expr1 -and expr2 cannot be true if the result of expr1 is false, so there is no point in performing expr2. Likewise, if we have the expression expr1 -or expr2 and the result of expr1 is true, there is no point in performing expr2, as we already know that the expression expr1 -or expr2 is true.

Okay, so this helps things go faster. Why is this important? Because we can rely on this behavior to control how actions are performed, as we shall soon see.

# Actions

Let’s get some work done! Having a list of results from our find command is useful, but what we really want to do is act on the items on the list. Fortunately, find allows actions to be performed based on the search results.

# Predefined Actions

There are a set of predefined actions and several ways to apply user-defined actions. First let’s look at a few of the predefined actions in Table 17-6.

# Table 17-6: Predefined find Actions

| Action | Description |
|---|---|
| -delete | Delete the currently matching file. |
| -ls | Perform the equivalent of ls -dils on the matching file. Output is sent to standard output. |
| -print | Output the full pathname of the matching file to standard output. This is the default action if no other action is specified. |