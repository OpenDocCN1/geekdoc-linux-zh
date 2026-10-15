
## Eliminating Duplicates with uniq

If you’ve sorted files using the handy-dandy sort command, you might end up with results that have duplicates in them. Heck, you might have files with duplicates. At any rate, here’s how to find and work with them. As Code Listing 6.18 shows, you can get rid of duplicate lines by using the uniq command (short for “unique”) in conjunction with sort.

### Tips

- uniq finds only identical, adjacent (sorted) lines. For example, if you have both Jones and jones in your address book, uniq won’t identify either entry because they differ in capitalization.
- You can also use the -d flag to specify that you want to see only the duplicate lines. For example, say you want to see all of the people who are in both your carpool file and your nightout file. You’d just use sort carpool nightout | uniq -d.

### To eliminate duplicates with uniq:

- `sort address.book | uniq`

At the shell prompt, type sort and the filename, then type | uniq to pipe the output to uniq. The output of uniq will not contain any duplicated entries (Code Listing 6.18).

```
[ejr@hobbes manipulate]$ more long.address.book
Schmidt, Sven, 1 Circle Drive, Denver, CO, 80221, 555-555-8382
Feldman, Fester, RR1, Billings, MT 62832, 285-555-0281
Brown, John, 1453 South Street, Tulsa, OK, 74114, 918-555-1234
Smith, Sally, 452 Center Ave., Salt Lake City, UT, 84000, 801-555-8982
Jones, Kelly, 14 Main Street, Santa Clara, CA, 95051, 408-555-7253
Schmidt, Sven, 1 Circle Drive, Denver, CO, 80221, 555-555-8382
Feldman, Fester, RR1, Billings, MT 62832, 285-555-0281
Brown, Jonathon, 1453 South Street, Tulsa, OK, 74114, 918-555-1234
Smith, Sally, 452 Center Ave., Salt Lake City, UT, 84000, 801-555-8982
Jones, Kelly, 14 Main Street, Santa Clara, CA, 95051, 408-555-7253
[ejr@hobbes manipulate]$ sort long.address.book | uniq
Brown, John, 1453 South Street, Tulsa, OK, 74114, 918-555-1234
Feldman, Fester, RR1, Billings, MT 62832, 285-555-0281
Jones, Kelly, 14 Main Street, Santa Clara, CA, 95051, 408-555-7253
Schmidt, Sven, 1 Circle Drive, Denver, CO, 80221, 555-555-8382
Smith, Sally, 452 Center Ave., Salt Lake City, UT, 84000, 801-555-8982
[ejr@hobbes manipulate]$
```

Code Listing 6.18 Use sort with uniq to eliminate duplicates.

## Redirecting to Multiple Locations with tee

Suppose you just updated your address book file and want to send it to your boss in addition to putting it in your own files. You can, using tee, which redirects output to two different places (see Code Listing 6.19).

### To redirect output to two locations with tee:

- `sort address.book new.addresses | tee sorted.all | mail boss@raycomm.com -s "Here's the address book, boss" -`

At the shell prompt, use the tee command plus a filename in the middle of the pipe line to send the sorted information to that filename as well as to the standard output (which could, of course, be redirected to another filename). Here, we send the results of the sort to the sorted.all file and to standard output, where mail will take over and send the file to the boss (see Chapter 11 for more on fancy mail tricks).

### Tee Time?

You might think of the tee command as being similar to a plumber's pipe joint—that is, it takes stuff from one location and sends it out to two different places.

```
[ejr@hobbes manipulate]$ sort address.book new.addresses | tee sorted.all | mail boss@raycomm.com -s "Here's the address book, boss"
[ejr@hobbes manipulate]$
```

Code Listing 6.19 Use tee to send output to two different places at once.

## Changing with tr

Sometimes you just have to make changes to a file to change all occurrences of one term or character to another. For example, you might have reversed the case in a file (by accidentally typing with Caps Lock on...argh!) and need to repair it. Or you might want to turn a document into a list of words (one per line) that you can sort or count. The tr utility is just what you need (see Code Listing 6.20).

### To translate case with tr:

- `cat limerick | tr a-zA-Z A-Za-z`

At the shell prompt, use the cat command and the pipe to send a file to tr, which will then translate lowercase to uppercase, and vice versa.

### To break lines with tr:

- `cat limerick | tr -c a-zA-Z "\n"`

Change anything that's not a letter (upper or lowercase) to a new line, thus breaking the limerick into a list of words. The -c indicates that anything that does not match the first set of characters (the complement of those characters) should be changed to the new character.

```
[jdoe@frazz jdoe]$ cat limerick
There once was a man from Nantucket.
Who carried his lunch in a bucket,
Said he with a sigh,
As he ate a whole pie,
If I just had a donut I'd dunk it.

[jdoe@frazz jdoe]$ cat limerick | tr 'a-zA-Z' 'A-Za-z'
THERE ONCE WAS A MAN FROM nANTUCKET.
WHO CARRIED HIS LUNCH IN A BUCKET,
SAID HE WITH A SIGH,
AS HE ATE A WHOLE PIE,
IF I JUST HAD A DONUT I'D DUNK IT.

[jdoe@frazz jdoe]$ cat limerick | tr -c 'a-zA-Z' '\n'
There
once
was
a
man
from
Nantucket

Who
carried
his
lunch
in
a
bucket

Said
he
with
a
sigh

As
he
ate
a
whole
pie

If
I
just
had
a
donut
I
d
dunk
it
```

Code Listing 6.20 Use tr to translate characters in files.
