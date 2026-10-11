# CRUNCH

**Tool Authors:** Mimayin, Bofh28

**Tool Website:** [https://sourceforge.net/projects/crunch-wordlist/](https://sourceforge.net/projects/crunch-wordlist/)

Crunch is a great program that allows you to create your own custom password lists. Simple tell crunch what you want, the length and complexity, and Crunch makes it for you.

```
(kali@kali)-[~]
$ crunch -h
crunch version 3.6

Crunch can create a wordlist based on criteria you specify.
The output from crunch can be sent to the screen, file, or
to another program.

Usage: crunch <min> <max> [options]
where min and max are numbers

Please refer to the man page for instructions and examples on how to use crunch.
```

The Crunch manual page (in a Kali terminal, enter `man crunch`) contains complete instructions and examples on how to use the tool. Basically, all we need to tell crunch is the minimum and maximum length of the words, what type of characters to use, and Crunch does the rest. Crunch makes heavy use of the *charset.lst* file that is located in its install directory - “/etc/share/crunch”. So, you will need to either run crunch from that directory or point to the directory with the “-f” switch when using the more advanced character sets (shown below).

Alright, let’s start with an easy one:

```
> At a terminal prompt, type, `crunch 1 3 -o threeletters.txt`
```