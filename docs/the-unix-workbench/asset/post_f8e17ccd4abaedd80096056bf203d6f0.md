
It looks like make successfully updated readme.txt! With every change to toc.txt, running make readme.txt will programmatically update readme.txt.

In order to simplify the make experience, we can create a rule at the top of our makefile called all where we can list all of the files that are built by the makefile. By adding the all target we can simply run make without any arguments in order to build all of the targets in the makefile. Let’s open up nano and add this rule:

```
nano makefile
```

```
all: draft_journal_entry.txt readme.txt

draft_journal_entry.txt:
    touch draft_journal_entry.txt

readme.txt: toc.txt
    echo "This journal contains the following number of entries:" > readme.txt
    wc -l toc.txt | egrep -o "[0-9]+" >> readme.txt
```

While we have nano open let’s add another special rule at the end of our makefile called clean which destroys the files created by our makefile:

```
all: draft_journal_entry.txt readme.txt

draft_journal_entry.txt:
    touch draft_journal_entry.txt

readme.txt: toc.txt
    echo "This journal contains the following number of entries:" > readme.txt
    wc -l toc.txt | egrep -o "[0-9]+" >> readme.txt

clean:
    rm draft_journal_entry.txt
    rm readme.txt
```

Let’s save and close our makefile then let’s test it out first let’s clean up our repository:

```
make clean
ls
```

```
## rm draft_journal_entry.txt
## rm readme.txt
## makefile
## toc.txt
```

```
make
ls
```

```
## touch draft_journal_entry.txt
## echo "This journal contains the following numb\
er of entries:" > readme.txt
## wc -l toc.txt | egrep -o "[0-9]+" >> readme.txt
## draft_journal_entry.txt
## readme.txt
## makefile
## toc.txt
```

Looks like our makefile works! The make command is extremely powerful, and this section is meant to just be an introduction. For more in-depth reading about make I recommend Karl Broman⁸’s tutorial⁹ or Chase Lambert¹⁰’s makefiletutorial.com¹¹.

## Summary

- make is a tool for creating relationships between files and programs, so that files that depend on other files can be automatically rebuilt.
- makefiles are text files that contain a list of rules.
- Rules are made up of targets (files to be built), commands (a list of bash commands that build the target), and dependencies (files that the target depends on to be built).

⁸https://twitter.com/kwbroman
⁹http://kbroman.org/minimal_make/
¹⁰http://chaselambda.com
¹¹http://makefiletutorial.com

## Bash Programming

> Communities begin by building their kitchen. -
> French proverb

The last two chapters have discussed how to use the bash shell. Bash itself is a little programming language, and this chapter we’re going to discuss how you can write your own computer programs in Bash. Programming in Bash is useful to know because of how seamlessly it integrates with all of the command line programs you’ve already learned. By the end of this chapter you should be able to write your own command line tools!

You can use nano to write all of the programs we’re going to discuss in this chapter, however I recommend using the Atom text editor because it’s more user friendly.

Now let’s create a new file called math.sh in the ~/Code/ directory and let’s open that file with either nano or Atom.

```
cd ~/Code/
nano math.sh
```

You should now have a new, clean text file open. Any code block in the following chapters that starts with the code (or similar) below should indicate to you that we’re working on a particular text file.

You do not need to add these lines to your file, though you should type exactly what I have typed below these lines. Note: please type all of the lines out for every program that we’re going to write, do not copy and paste. Typing code is a little different from typing an email, and you should practice typing the code out yourself as much as possible. Both of these lines start with the pound symbol (#) and in the Bash programming language anything that is typed after a pound symbol is ignored (unless the pound symbol is between curly brackets ({ }), but that’s only in very specific situations). The pound symbol allows you to make comments in your code which you can use to annotate code so that another human being who is reading your code can understand how your program is designed to function.

If you’re using nano or another shell-based text editor you should perhaps open up two terminals, one where you can edit and save the programs you’re working on, and one where you can run your programs. One advantage of using Atom is that you can keep Atom open in a separate window and then run your programs in your terminal window.

## Math

The Bash programming language can do very basic arithmetic, which we’ll demonstrate in this section. Now that you have math.sh open in your preferred text editor type the following into your text editor:
