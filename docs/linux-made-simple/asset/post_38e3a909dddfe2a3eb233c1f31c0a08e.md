
## Terminal: Time-savers

The terminal has a host of handy tricks that will save you time and make your life easier. Let’s introduce a few of the most useful techniques.

Earlier, we mentioned that using the terminal can be faster and more productive than using a GUI, especially with repeated operations. To get the most out of this, it helps to know a few of the shell’s secrets.

Do you often find yourself typing in the same command options over and over again? Do you sometimes have trouble remembering the correct options? Are you just plain lazy and want to avoid typing wherever possible? If you answered yes to any of these, aliases are for you. You already have some shell aliases set up. To list them, type:

```
alias
```

which will return entries like this (from Ubuntu):

```
alias ll='ls -alF'
```

```
alias ls='ls --color=auto'
```

The first of these examples is simple – if you type in ll, it runs ls -alF. The second is cleverer, because the alias is the same as the command name, so the old ls behaviour disappears and it’s always run with the --color=auto option. If you find yourself always using certain options with particular commands, aliases like this effectively make those options the defaults. The alias is expanded before the rest of the command line is interpreted, so:

```
ll X Y Z
```

becomes

```
ls -alF X Y Z
```

These aliases aren’t always easy to remember, but fear not – you can create your own aliases using exactly the same syntax as in the output from the alias command:

```
alias myalias='somecommand --option1 --option2'
```

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_113_0.png)

Aliases save you typing and enable you to use more memorable command abbreviations. You choose these yourself, so you have no excuse for forgetting!

Aliasing a command to its own name is a neat trick, but what if you then need to use the original command? Don’t worry – the developers have thought of that. Prefix the command with a backslash and your alias will be ignored:

```
\ls Documents
```

### Profiles

You can customise your terminal experience with aliases and custom prompts, but to make them even more convenient, you need a way of applying these automatically when you open a terminal. That can be done through your profile, which is a file containing commands that are read and run whenever you open a shell session.

There are several locations that are read, the first of which is /etc/profile, which contains global profile settings. This in turn runs any files in /etc/profile.d, which makes it easy to add global settings without touching the default profile. Then the user’s profile is read from one of ~/.bash_profile, ~/.bash_login and ~/.profile. Only the first of these files that exists is run, and any settings in here override those in the global profile if the same thing is set in both.

The profile is simply a set of shell commands, one per line, that are run when the shell starts up. These can set up aliases or environment variables, or set the command prompt. A typical use of environment variables would be to change the default text editor to nano:

```
EDITOR=/usr/bin/nano
```

### Word completion

If you aren’t a particularly confident touch typist, you’ll soon get fed up with typing out command and file names in full, then dealing with the error messages resulting from misspellings. Fortunately, the shell provides a way to both save typing and avoid mistakes, called tab completion. The name is fairly self-explanatory – it uses the [Tab] key to complete the word you are typing. If this is the first word on a line, it will be a command, so it looks in the command path for matches – for example, typing chm and hitting [Tab] will complete to chmod. Used after the command, hitting [Tab] completes file names, so instead of typing:

```
cat /pathto/somelongdirectory/someevenlongerfilename.txt
```

you can use:

```
cat /pa[Tab]som[Tab]som[Tab]
```

Isn’t that easier? When more than one file matches, the [Tab] key will complete up to the point where it becomes ambiguous; pressing [Tab] again at this point shows a list of options, which you can cycle through with [Tab], or add another letter or two and press [Tab] again. It is actually a lot easier to use than to describe – just try it.

### Wild, wild cards

There are times you want to include more than one file in a command, but don’t want to type them all out. The Linux shell has a couple of wildcard operators to help you out with this. The most frequently used one is the star, which is used as a replacement for any string of characters. So * on its own will match every file in the current directory (note that this is different from MS-DOS shells, where * does not match . and you need to use *.* to match any file with an extension). You can also use * to match one part of a file name – *.txt matches all files that end with .txt, and a*.txt only matches those that also start with a. This matching is performed by the shell. It expands the matches to a list of files before passing them to the command, which never sees the wildcard or even knows that you’ve used one. This can be an important distinction, especially if you want to pass a * to the program you’re running. For example, if you’re using scp to copy files from a remote computer and run:

```
scp user@othercomputer:Documents/*.txt Documents/
```

you may expect it to copy all .txt files from the other computer’s Documents directory to the same one here, but it won’t. The shell expands the *.txt to match all .txt files on the local system, so you only copy the files you already have. In such an instance, you need to tell the shell not to expand the * by preceding it by a backslash, known as escaping it:

```
scp user@othercomputer:Documents/\*.txt Documents/
```

Now it passes Documents/*.txt unchanged to the remote computer and lets its shell handle the expansion.

There’s a second wildcard character. While * matches any number of characters, including none, ? matches exactly one. So ab?.txt matches abc.txt and ab1.txt but not ab.txt or abcd.txt, whereas ab*.txt would match all of them.

### Bring on the substitute

There is a powerful feature in shells called command substitution. This allows you to embed the output from one command in another. As a simple example, there is a command called foo on your system, and let’s say you want to know what type of program it is: compiled, Python or even a shell script. The which command gives you the path to a program, and file reports the type of a file. You could use:

```
which foo
```

to get /usr/local/bin/foo and then

```
file /usr/local/bin/foo
```

to get the file type, but even with copy and paste, this is a lot of work and easy to mistype. Alternatively, you could do:

```
file $(which foo)
```

```
/usr/local/bin/foo: a /usr/bin/perl script, ASCII text executable
```

What happens is that the shell runs whatever is inside $(...) and substitutes the output from that into the command line before running it. You can also use backticks for this:

```
file `which foo`
```

This is quicker to type but less readable, especially when posted to a forum where the reader’s font can make ` and ’ look similar. With the first format there is no such confusion.

One of the great advantages of the shell is that it’s simple to repeat commands, no matter how complex, with a couple of keypresses. At its simplest, you can press the [Up] key to show previous commands, then press [Enter] to run your chosen one again. You can also edit the command before running it, if you like. That’s fine if you want to use one of the last few commands you ran, but most shells keep a history of the last 500 or so commands that you can access again.

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_114_0.png)

As the name suggests, tab completion lets you use the [Tab] key to complete the word you’re typing, helping save time and avoid mistakes.

### Please repeat that

To avoid wearing out your keyboard’s [Up] arrow key (and your eyes), press [Ctrl]+[R] and then type in part of the command. The terminal will now show you the most recent command that matches what you are typing, updating with each keypress you make. If you have run several very similar commands, you don’t need to keep typing – just type a few characters and press [Ctrl]+[R] again to see the previous match.

Keep going until you find the one you want. (Don’t be alarmed – this is one of those things that takes far longer to describe than to actually do.) You can edit the command before running it. The search term that you type in doesn’t have to be the command itself – any part of the command line will match, so you could start with the file name.

You can also access commands within the history directly. The ! character tells the shell that you are referring to its history. !! is a shortcut for the previous command, while !n means ‘execute the command run n commands ago’ (so !! is the same as !-1). !xyz runs the last command starting with xyz, and !?xyz does the same for the last command containing xyz (much the same as [Ctrl]+[R]).

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_114_1.png)

The history command shows recently executed commands – use ! and [Ctrl]+[R] to find and run again the commands you used before.
