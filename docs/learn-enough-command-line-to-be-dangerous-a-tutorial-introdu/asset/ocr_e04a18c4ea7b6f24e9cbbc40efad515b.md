```
$ ls fooba<tab>
foobarquux foobazquux
```

We could then type more letters to resolve the ambiguity, so typing the r after **fooba** and hitting `<tab>` would yield

```
$ ls foobar<tab>
```

which would be completed to **foobarquux**. This situation is common enough that experienced command-line users will often just hit something like f<tab><tab> to get the shell to show all the possibilities:

```
$ ls f<tab><tab>
figure_1.png  foobarquux   foobazquux
```

Additional letters would then be typed as usual to resolve the ambiguity.

The default behavior of **rm** on an unconfigured Unix system is actually to remove the file without confirmation, but (because deletion is irreversible) many systems *alias* the **rm** command to use an option to turn on confirmation. (As you can verify by running **man rm**, this option is **-i**, so in fact **rm** is really **rm -i**.) There are many situations where confirmation is inconvenient, though, such as when you’re deleting a list of files and don’t want to have to confirm each one. This is especially common when using the wildcard \* introduced in Section 2.2. For example, to remove all the files ending with “.txt” using a single command, *without* having to confirm each one, you can type this:

```
$ rm -f *.txt
```

Here **-f** (for “force”) overrides the implicit **-i** option and removes all files immediately. (**N.B.** You are now in a position to understand the command in Figure 2.)

39