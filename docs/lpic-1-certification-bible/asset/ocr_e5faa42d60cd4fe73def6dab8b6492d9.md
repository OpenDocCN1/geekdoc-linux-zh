If you wish to redirect only stderr to a file, then you would use the 2> symbols. For example, to redirect only the stderr for the sort command used previously, use the following:

```
sort namelist 2> namelisterrrs
```

This is also useful if you wish to run a command while redirecting stderr and stdout to two separate files. The following example would send stderr to the namelisterrrs file while sending stdout to the sortednamelist file.

```
sort namelist 2> namelisterrrs > sortednamelist
```

# Pipes

Along with redirecting data to a file, you may want to use other commands at times. This procedure can be done using the pipes character (|). This allows you to use one command line to send output data from one command as input data to another. In the following example, the file namelist is sorted alphabetically, and then line numbers are added to each name using the nl command.

```
# sort +1 namelist | nl
1 Peter Anapol
2 Jeff Arellano
3 Scott Bessler
4 Alex Blauvelt
5 Michael Craig
6 Joakim Erdfelt
7 Johannes Erdfelt
8 Pete Gizzi
9 David Goosby
10 Thomas McCanta
11 Angie Nash
12 Jason Nash
13 Neil Schroeder
14 Derek Stutsman
15 Paul Ward
```

This data can also be piped into another utility or redirected to a file.

```
# sort +1 namelist | nl > numberrednames
# more numberrednames
1 Peter Anapol
2 Jeff Arellano
3 Scott Bessler
4 Alex Blauvelt
5 Michael Craig
6 Joakim Erdfelt
7 Johannes Erdfelt
```