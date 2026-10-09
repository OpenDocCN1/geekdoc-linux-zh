```
$ touch uno due tre quattro cinque sei sette otto nove dieci
```

+   Use the ls command just to list them all (by default, it lists them by name in alphabetical order):

```
$ ls
cinque dieci due nove otto quattro sei sette tre uno
```

+   3. Now let's group them in a number of different ways, using the metacharacters we just mentioned. First, list all the files that start with the letter s:

```
$ ls s*
sei sette
```

+   4. Next, use the ? metacharacter to select all files whose name consists of exactly three characters:

```
$ ls ???
due sei tre uno
```

+   5. Next, select all the files whose name starts with a vowel:

```
$ ls [aeiou]*
otto uno
```

+   6. Next, select all the files whose name starts with any character in the range a to f:

```
$ ls [a-f]*
cinque dieci due
```

+   7. Finally, select all the files whose name *does not* start with a vowel. The exclamation operator must be within the square parentheses.

```
$ ls [!aeiou]*
cinque dieci due nove quattro sei sette tre
```

# How It Works

We've used the ls command here to demonstrate file globbing, because the output from ls shows the effects of the globbing very clearly. However, you should note that we can use file globbing with any command that expects filename or directory-name arguments. Let's look at each of the globbing expressions here.