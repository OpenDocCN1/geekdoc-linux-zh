
# Hour 9

4. I could revise my alias, but trying to get the quotation marks correct is a nightmare.
It would be much easier to make this simple shell script instead:

```
% cat bin/wrongs
# wrongs - show a list of commonly misused words in the file

cat $* | \
awk '{for (i=1;i<=NF; i++) print $i}' | \
fgrep -F ".wrongs"
```

To make this work, I need to remove the existing aliases for wrongwords
using the C shell alias, add execute permission to the shell script, and
then rehash to ensure that the C shell can find the command when requested:

```
% alias wrongwords
% chmod +x bin/wrongwords
% rehash
```

Now it's ready to use:

```
% wrongwords sample3
insure
afect
```

5. The fgrep command can also exclude words from a list. If you have been using
the myspell command, it's quite clear that the program doesn't know anything about
acronyms or some other correctly spelled words that you might use in your writing.
Where that grep can be a helpful patriot. Build a list of words that you
commonly use that aren't misspelled but that spell reports as being misspelled:

```
% alias myspell '*spell\* | fgrep -v -f $HOME/.dictionary'
% cat $HOME/.dictionary
BBS:
FAX
Taylor
Utech
ygote
```

Now spell can be more helpful:

```
% spell newsample
FAX
illiterate
Literacy
letteracy
illiterate
Papert
pre
rithmetic
Rs
Taylor
Utech
ygote
% myspell newsample
illiterate
Literacy
```

# Wildcards and Regular Expressions

letteracy
letterate
Papert
pre
rithmetic
Rs

You have now met the entire family of grep commands. For the majority of searches for information, you can use the grep command itself. Sometimes, though, it's nice to have options, particularly if you decide to customize some of your commands as shown in the scripts and aliases explained in this hour.

# Task 9.7: Changing Things En Route with sed

I'm willing to bet that when you read about learning some UNIX programming tools in this, you anxious, your palms started to get sweaty, maybe your fingers shook, and the little voice in your head started to, “It's too late! We can use a pipe and paper! We don't need computers at all!

Don't panic.

If you think about it, you've programming all in UNIX. When you enter a command to the shell, you're programming the shell to perform immediately the task specified. When you specify file redirection or build a pipe, you're really writing a small UNIX program that the shell interprets and acts upon. Frankly, when you consider how many commands you know now and how many flags there are for each of the commands, you've quite a set of programming tools under your belt already, so onward!

With the | symbol called a pipe, and commands tied called pipelines, is it no wonder that the information flowing down a pipeline is a stream? For example, the command `cat test | wc` means that the cat command opens the file test and streams it to the wc, which counts the number of lines, words, and characters.

To edit, modify the information in a pipeline, then it seems reasonable to use a stream editor, and exactly what the sed command is! In fact, its name comes from its function: s for stream, and ed for editor.

Here's how the sed command is built on an old editor ed, the same editor that's responsible for the grep command Remember? The `global/regular expression/` prints exactly grep. A microcosm of unix itself, commands sed to separated by a semicolon.

There are many different sed commands, but keeping with my promise not to overwhelm you with options and variations that aren't going to be helpful, I'll focus on using sed to substitute one pattern for another and for extracting ranges of lines from a file. The general format of the substitution command is: `s/old/new/flags`, where old and new are the patterns

you're working with, s is the abbreviation for the substitute command, and the two most
helpful flags are g (to replace all occurrences globally on each line) and n (to tell sed to replace
the first n occurrences of the pattern). By default, lines are listed to the screen, so a sed
expression like 10q will cause the program to list the first 10 lines and quit (making
an alternative to the command head -10). Deletion is: the command is preceded by
one or two addresses in the file, reflecting a request to delete either lines that match the
specific address or all in the range of the first to last.

The format of the sed command is sed, followed by the expression in quotes, then, optionally,
tame of the file to read for input.

There are some examples:

- 1. I'll start with an example. I'll use sed to extract some lines from the /etc/
passwd file and then replace colons with a single space. The format of this
command is to substitute each occurrence of : with a space, or s/: / /
% sed tailor :/etc/passwd | sed -e "s/: /g"
tailor?: 1048:1375:Mary Tailor:/users/tailor:/bin/csh
tailor?: 769:1375:Mary Tailor:/users/tailor:/usr/local/lib/tcsh
tailor?: 375:3518:David Tailor:/users/tailor:/usr/local/lib/msh
tailor?: 203:1022:James Tailor:/users/tailor:/bin/csh
tailor?: 662:1042:Robert Tailor:/users/tailor:/bin/csh
tailor?: 869:1508:Melanie Tailor:/users/tailor:/bin/csh
tailor?: 1989:1412:David Tailor:/users/tailor:/bin/csh

This doesn't do what I want because I needed to append the global
instruction to the sed command to ensure that it would replace all occurrences of
each line. I'll try it, this time adding a g to the instruction.

```
% sed tailor :/etc/passwd | sed -e "s/: /g"
tailor?: 1048:1375:James Tailor:/users/tailor:/bin/csh
tailor?: 769:1375:Mary Tailor:/users/tailor:/usr/local/lib/tcsh
tailor?: 375:3518:David Tailor:/users/tailor:/usr/local/lib/msh
tailor?: 203:1022:James Tailor:/users/tailor:/bin/csh
tailor?: 662:1042:Robert Tailor:/users/tailor:/bin/csh
tailor?: 869:1508:Melanie Tailor:/users/tailor:/bin/csh
tailor?: 1989:1412:David Tailor:/users/tailor:/bin/csh
```

- 2. A more sophisticated example of substitution would be to replace all occurrences of
Tailor with Taylor:

```
% sed tailor :/etc/passwd | sed -e "s/Tailor:/g"
tailor?: 1048:1375:James:/users/tailor:/bin/csh
tailor?: 769:1375:Mary:/users/tailor:/usr/local/lib/tcsh
tailor?: 375:3518:David:/users/tailor:/usr/local/lib/msh
tailor?: 203:1022:James:/users/tailor:/bin/csh
tailor?: 662:1042:Robert:/users/tailor:/bin/csh
tailor?: 869:1508:Melanie:/users/tailor:/bin/csh
tailor?: 1989:1412:David:/users/tailor:/bin/csh
```
