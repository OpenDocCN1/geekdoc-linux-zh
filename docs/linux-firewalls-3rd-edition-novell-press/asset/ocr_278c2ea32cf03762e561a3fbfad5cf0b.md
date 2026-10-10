For determining the current host, this is the syntax:

```
`@@ifhost <hostname>`
```

The negation for the `@@ifhost` evaluation is, as you might guess, the following:

```
`@@ifnhost <hostname>`
```

Regardless of which control structure is used, it must be closed using the statement:

```
`@@endif`
```

Multiple control structures can be grouped using an `else` type of structure that you would expect for an associated `if` statement. The syntax is simply as follows:

```
`@@else`
```

Here's an example of how each of these might be used. The first example checks to see whether the macro called `SOURCE` has been defined, and if not, defines it:

```
`@@ifndef SOURCE`
`@@define SOURCE /usr/src`
`@@endif`
```

The second example looks at the hostname of the computer from which AIDE is being run and sets a macro based on the results of that check. This might be helpful if you have differing directory structures between various hosts and you'd like to use only one common AIDE configuration file among them. Here's the second example:

```
`@@ifhost netserver`
`@@define LOCALBINDIR /usr/local/sbin`
`@@endif`
```

Finally, here is an example using an `else` statement:

```
`@@ifhost netserver`
`@@define LOCALBINDIR /usr/local/sbin`
`@@ELSE`
`@@define LOCALBINDIR /usr/local/bin`
`@@endif`
```

For all the examples, recall that you'd use these macros later within the configuration using the following syntax:

```
`@@{<macro>}`
```