# Chapter 6 Passing Arguments

```
$ cat phonebook
Alice Chebbe 973-555-2015
Barbara Swingle 201-555-9257
Liz Stachiw 212-555-2298
Susan Goldberg 201-555-7776
Susan Topple 212-555-4932
Tony Iannino 973-555-1295
Stromboli Pizza 973-555-9478
$
```

See what happened

Stromboli Pizza was quoted so that the shell passed it to add as a single argument (what would have happened if it wasn't quoted?). After finishing execution, I ran to see if it could affect the new entry, and to edit. The cat command was executed to see what the modified phonebook file looked like. The new entry was added to the end, as intended.

Unfortunately, the new file is no longer sorted. This will not affect the operation of the program but it's a nice feature nonetheless. The solution? Adding sorting to the program by using the sort command:

```
$ cat add
# Add someone to the phonebook file -- version 2
#
```

```
echo "$1 \$2" >> phonebook
sort -o phonebook phonebook
$
```

Recall that the -o option to sort specifies what the sorted output is to be written, and that this can be the same as the input file:

```
$ add 'Billy Bach' 201-555-7618
$ cat phonebook
Alice Chebbe 973-555-2015
Barbara Swingle 201-555-9257
Billy Bach 201-555-7618
Liz Stachiw 212-555-2298
Stromboli Pizza 973-555-9478
Susan Goldberg 201-555-7776
Susan Topple 212-555-4932
Tony Iannino 973-555-1295
$
```

Each time a new entry is added, the phonebook file will get re-sorted so that multi-line matches are always in alphabetical order.