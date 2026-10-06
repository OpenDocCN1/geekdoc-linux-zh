If the pattern does not exist in the specified file(s), the **grep** command simply displays nothing:

```
$ grep cracker ed.cmd
$
```

You saw in the section on **sed** how you could print all lines containing the string UNIX from the file *intro* with the command

```
sed -n '/UNIX/p' intro
```

But you could also use the following **grep** command to achieve the same result:

```
grep UNIX intro
```

Recall the phonebook line before from:

```
$ cat phonebook
Alice Cheba      973-555-2015
Barbara Swingle  201-555-3378
Jeff Goldberg    212-555-2298
Liz Stazich
Susan Goldberg    201-555-7776
Tony Iannino     973-555-1295
$
```

When you need to look up a phone number, the **grep** command comes in handy:

```
$ grep Susan phonebook
Susan Goldberg 201-555-3776
$
```

The grep command is particularly useful when you have a lot of files and you want to find out which ones contain certain words or phrases. The following example shows how the **grep** command can be used to search for the word *shell* in *all* files in the directory:

```
$ grep shell *
cmfiles:shell that enables sophisticated
ed.cmd:files, and is independent of the shell.
ed.cmd:to the shell, just type in a q.
grep.cmd:occurrence of the word shell:
grep.cmd:$ grep shell *
grep.cmd:every use of the word shell.
$
```

As noted, when more than one file is specified to **grep**, each output line is preceded by the name of the file that line.

With expressions for **sed** and patterns for **tr**, it's a good idea to enclose your **grep** pattern inside a pair of single quotes to "protect" from the shell. It's an example of what can happen if you don't: say you want to find all the lines containing asterisks inside the file stars*: typing

```
grep * stars
```