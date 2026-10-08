# Advanced Bash-Scripting Guide

+   • The -- | "or" RE operator matches any of a set of alternate characters.

```
bash$ egrep 're(a|e)d' misc.txt
People who read to be better informed than those who do not.
The clarinet sounds by the vibration of its reed.
```

![](bbox=[0.121, 0.183, 0.153, 0.199])

Some versions of sed, ed, and ex escaped versions of the extended Regular Expressions described above, as the GNU units.

+   • POSIX Character Classes: [:class:]

This is an alternate method of specifying a range of characters to match.

+   • [:alnum:] matches alphanumeric or numeric characters. This is equivalent to A-Za-z0-9.
• [:alpha:] matches alphabetic characters. This is equivalent to A-Za-z.
• [:blank:] matches a space or tab.
• [:cntrl:] matches control characters.
• [:digit:] matches (decimal) digits. This is equivalent to 0-9.
• [:graph:] (printable characters). Matches characters in the range of ASCII 33 - 126. This is the same as [:print], but excluding the space character.
• [:lower:] matches lowercase alphabetic characters. This is equivalent to a-z.
• [:print:] (printable characters). Matches characters in the range of ASCII 32 - 126. This is the same as [:graph], but adding the space character.
• [:space:] matches whitespace characters (space and horizontal tab).
• [:upper:] matches uppercase alphabetic characters. This is equivalent to A-Z.
• [:xdigit:] matches hexadecimal digits. This is equivalent to 0-9-Fa-f.

> ! POSIX character classes generally require quoting or double brackets ([[]]).

```
bash$ grep [[:digit:]] test.file
abc=723
```

```
#
if [ $awrow ~ [[:digit:] ]]; # Numerical input?
then    # POSIX char class
    if [[ $acol =~ [:alpha:] ]]; # Number followed by a letter? Illegal!
fi
# # From ktour.sh example script.
```

These characters may be used with globbing, to a limited extent.

```
bash$ ls -l [[:digit:]]*
-rw-r-- 1 bozo 0 Aug 21 14:47 a33b
```

POSIX character classes are used in Example-16 and Example-22.

Sed, awk, and Perl, used as filters in scripts, take RE as arguments when "sifting" or transforming or I/O streams. Use Example-12 and Example-16 for illustrations of this.

The standard reference on this complex topic is Friedl's Mastering Regular Expressions. Sed & Aw, by Dougherty and Robbins, also gives a very lucid treatment of REs. See the Bibliography for more information on these books.

Chapter 18. Regular Expressions