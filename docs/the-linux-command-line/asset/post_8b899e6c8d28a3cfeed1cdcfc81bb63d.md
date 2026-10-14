
You can make this change permanent by adding this line to your `.bashrc` file:

```sh
export LANG=POSIX
```

## POSIX Basic Vs. Extended Regular Expressions

Just when we thought this couldn’t get any more confusing, we discover that POSIX also splits regular expression implementations into two kinds: *basic regular expressions (BRE)* and *extended regular expressions (ERE)*. The features we have covered so far are supported by any application that is POSIX-compliant and implements BRE. Our `grep` program is one such program.

What’s the difference between BRE and ERE? It’s a matter of metacharacters. With BRE, the following metacharacters are recognized:

`^  $  .  [  ]  *`

All other characters are considered literals. With ERE, the following metacharacters (and their associated functions) are added:

`(  )  {  }  ?  +  |`

However (and this is the fun part), the “(”, “)”, “{”, and “}” characters are treated as metacharacters in BRE if they are escaped with a backslash, whereas with ERE, preceding any metacharacter with a backslash causes it to be treated as a literal. Any weirdness that comes along will be covered in the discussions that follow.

Since the features we are going to discuss next are part of ERE, we are going to need to use a different `grep`. Traditionally, this has been performed by the `egrep` program, but the GNU version of `grep` also supports extended regular expressions when the `-E` option is used.

> ### POSIX
> 
> During the 1980’s, Unix became a very popular commercial operating system, but by 1988, the Unix world was in turmoil. Many computer manufacturers had licensed the Unix source code from its creators, AT&T, and were supplying various versions of the operating system with their systems. However, in their efforts to create product differentiation, each manufacturer added proprietary changes and extensions. This started to limit the compatibility of the software.

As always with proprietary vendors, each was trying to play a winning game of “lock-in” with their customers. This dark time in the history of Unix is known today as “the Balkanization.”

Enter the IEEE (Institute of Electrical and Electronics Engineers). In the mid-1980s, the IEEE began developing a set of standards that would define how Unix (and Unix-like) systems would perform. These standards, formally known as IEEE 1003, define the application programming interfaces (APIs), shell and utilities that are to be found on a standard Unix-like system. The name “POSIX,” which stands for Portable Operating System Interface (with the “X” added to the end for extra snappiness), was suggested by Richard Stallman (yes, that Richard Stallman), and was adopted by the IEEE.

## Alternation

The first of the extended regular expression features we will discuss is called alternation, which is the facility that allows a match to occur from among a set of expressions. Just as a bracket expression allows a single character to match from a set of specified characters, alternation allows matches from a set of strings or other regular expressions.

To demonstrate, we’ll use grep in conjunction with echo. First, let’s try a plain old string match:

```
[me@linuxbox ~]$ echo "AAA" | grep AAA
AAA
[me@linuxbox ~]$ echo "BBB" | grep AAA
[me@linuxbox ~]$
```

A pretty straightforward example, in which we pipe the output of echo into grep and see the results. When a match occurs, we see it printed out; when no match occurs, we see no results.

Now we’ll add alternation, signified by the vertical bar metacharacter:

```
[me@linuxbox ~]$ echo "AAA" | grep -E 'AAA|BBB'
AAA
[me@linuxbox ~]$ echo "BBB" | grep -E 'AAA|BBB'
BBB
[me@linuxbox ~]$ echo "CCC" | grep -E 'AAA|BBB'
[me@linuxbox ~]$
```

Here we see the regular expression `AAA|BBB` which means “match either the string AAA or the string BBB.” Notice that since this is an extended feature, we added the `-E` option to grep (though we could have just used the egrep program instead), and we enclosed the regular expression in quotes to prevent the shell from interpreting the vertical bar metacharacter as a pipe operator. Alternation is not limited to two choices:

```sh
[me@linuxbox ~]$ echo "AAA" | grep -E 'AAA|BBB|CCC'
AAA
```

To combine alternation with other regular expression elements, we can use () to separate the alternation:

```sh
[me@linuxbox ~]$ grep -Eh '^(bz|gz|zip)' dirlist*.txt
```

This expression will match the filenames in our lists that start with either “bz”, “gz”, or “zip”. Had we left off the parentheses, the meaning of this regular expression :

```sh
[me@linuxbox ~]$ grep -Eh '^bz|gz|zip' dirlist*.txt
```

changes to match any filename that begins with “bz” or contains “gz” or contains “zip”.

## 20 – Regular Expressions

## Quantifiers

Extended regular expressions support several ways to specify the number of times an element is matched.

### ? - Match An Element Zero Or One Time

This quantifier means, in effect, “make the preceding element optional.” Let’s say we wanted to check a phone number for validity and we considered a phone number to be valid if it matched either of these two forms:

- `(nnn) nnn-nnnn`
- `nnn nnn-nnnn`

where “n” is a numeral. We could construct a regular expression like this:

```text
^\([0-9][0-9][0-9]\)? [0-9][0-9][0-9]-[0-9][0-9][0-9][0-9]$
```

In this expression, we follow the parentheses characters with question marks to indicate that they are to be matched zero or one time. Again, since the parentheses are normally
