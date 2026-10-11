# EXPLANATION (CONTINUED)

6  The line containing the regular expression $Lori$ is printed.

7  The $seek$ function will position the file pointer for $fh$ at the byte offset. $Scurrtentpos$, +40 bytes from the beginning of the file. Without $seek$, there is no way to go directly to byte 40; the only option would be to start again from the beginning of the file.

8  The lines starting at offset 40 are read in and stored in the array @$lines@.

9  The array is printed, starting at offset 40.

# 10.2.13  Opening for Reading and Writing

Two files are used in the next example: a text file, called $visitor.txt$, which has an initial value of 1 as its only text, and $countem.pl$, the script that will be used to track the number of users who have run the script.

The $visitor\_count$ file is a Perl script that will add one to the $visitor.txt$ file every time the script is executed.

Table 10.2  Reading and Writing Operations

| Symbol  | Open For                                 |
|---------|------------------------------------------|
| +<      | Read first, then write.                  |
| +>      | Write first, then read (>) clobbers your file). |
| +>>     | Append first, then read.                 |

# EXAMPLE 10.28

(The text file, visitor.txt)

1

(The Script)

```
use warnings;
# Scriptname: countem.pl
# Open visitor.count for reading first, and then writing
1  open(my $fh, "+<", "visitor.txt") ||
   die "Can't open visitor.txt: $!\n";
2  $count=<<$fh>;                # Read a number back to the top of the file
3  print "You are visitor number $count.";
4  $count<+;
5  seek($fh, 0,0) || die;       # Seek back to the top of the file
6  print $fh $count;             # Write the new number to the file
7  close $fh;
```