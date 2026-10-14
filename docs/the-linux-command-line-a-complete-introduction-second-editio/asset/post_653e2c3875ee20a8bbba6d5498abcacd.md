
you need. The Erector Set takes on the shape of your imagination.
It does what you want.

Your choice of toys is, of course, a personal thing, so which toy would you find more satisfying?

## 7

## SEEING THE WORLD AS THE SHELL SEES IT

![](img/314a0280bc10c5c0d45be132de172677_111_0.png)

In this chapter, we are going to look at some of the “magic” that occurs on the command line when we press the ENTER key. While we will examine several interesting and complex features of the shell, we will do it with just one new command:

echo Display a line of text

### Expansion

Each time we type a command and press the ENTER key, bash performs several substitutions upon the text before it carries out our command. We have seen a couple of cases of how a simple character sequence, for example *, can have a lot of meaning to the shell. The process that makes this happen is called expansion. With expansion, we enter something, and it is expanded into something else before the shell acts upon it. To demonstrate what we mean by this, let’s take a look at the echo command. echo is a shell builtin that performs a very simple task. It prints its text arguments on standard output.

```
[me@linuxbox ~]$ echo this is a test
this is a test
```

That’s pretty straightforward. Any argument passed to echo gets displayed. Let’s try another example.

```
[me@linuxbox ~]$ echo *
Desktop Documents ls-output.txt Music Pictures Public Templates Videos
```

So what just happened? Why didn’t echo print *? As we recall from our work with wildcards, the * character means match any characters in a filename, but what we didn’t see in our original discussion was how the shell does that. The simple answer is that the shell expands the * into something else (in this instance, the names of the files in the current working directory) before the echo command is executed. When the ENTER key is pressed, the shell automatically expands any qualifying characters on the command line before the command is carried out, so the echo command never saw the *, only its expanded result. Knowing this, we can see that echo behaved as expected.

### Pathname Expansion

The mechanism by which wildcards work is called pathname expansion. If we try some of the techniques that we employed in earlier chapters, we will see that they are really expansions. Given a home directory that looks like this:

```
[me@linuxbox ~]$ ls
Desktop   ls-output.txt   Pictures   Templates
Documents Music           Public     Videos
```

we could carry out the following expansions:

```
[me@linuxbox ~]$ echo D*
Desktop Documents
```

and this:

```
[me@linuxbox ~]$ echo *s
Documents Pictures Templates Videos
```

or even this:

```
[me@linuxbox ~]$ echo [[:upper:]]*
Desktop Documents Music Pictures Public Templates Videos
```

and looking beyond our home directory, we could do this:

```
[me@linuxbox ~]$ echo /usr/*/share
/usr/kerberos/share /usr/local/share
```

### PATHNAME EXPANSION OF HIDDEN FILES

As we know, filenames that begin with a period character are hidden. Pathname expansion also respects this behavior. An expansion such as the following does not reveal hidden files:

```
echo *
```

It might appear at first glance that we could include hidden files in an expansion by starting the pattern with a leading period, like this:

```
echo .*
```

It almost works. However, if we examine the results closely, we will see that the names . and .. will also appear in the results. Because these names refer to the current working directory and its parent directory, using this pattern will likely produce an incorrect result. We can see this if we try the following command:

```
ls -d .* | less
```

To better perform pathname expansion in this situation, we have to employ a more specific pattern.

```
echo .[!.]*
```

This pattern expands into every filename that begins with only one period followed by any other characters. This will work

correctly with most hidden files (though it still won’t include filenames with multiple leading periods). The ls command with the -A option (“almost all”) will provide a correct listing of hidden files.

```
ls -A
```

### Tilde Expansion

As we may recall from our introduction to the cd command, the tilde character (~) has a special meaning. When used at the beginning of a word, it expands into the name of the home directory of the named user or, if no user is named, the home directory of the current user.

```
[me@linuxbox ~]$ echo ~
/home/me
```

If user “foo” has an account, then it expands into this:

```
[me@linuxbox ~]$ echo ~foo
/home/foo
```

### Arithmetic Expansion

The shell allows arithmetic to be performed by expansion. This allows us to use the shell prompt as a calculator.

```
[me@linuxbox ~]$ echo $((2 + 2))
4
```

Arithmetic expansion uses the following form:

```
$((expression))
```

where expression is an arithmetic expression consisting of values and arithmetic operators.
