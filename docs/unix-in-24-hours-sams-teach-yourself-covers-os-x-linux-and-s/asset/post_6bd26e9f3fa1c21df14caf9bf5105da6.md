
3. Let’s do a quick analysis of what shells people are using by pulling out the seventh field with cut and then piping it to sort and uniq with the important -c flag to have uniq show a count of matching results:

Click here to view code image

```
$ cut -d: -f7 /etc/passwd | sort | uniq -c
  51 /bin/bash
  857 /bin/csh
   40 /bin/ksh
    1 /bin/sh
  382 /bin/tcsh
    9 /bin/zsh
    8 /noshell
    5 /usr/local/bin/bash
    7 /usr/local/bin/tcsh
$
```

## Note

If you want to have the output sorted from most popular to least popular, you can use another sort on the end of the pipe: sort -rn will sort in reverse numerical order. This means that the line prefaced with the largest number (/bin/csh) will appear first, and the line prefaced with the smallest number (/bin/sh) will appear last.

4. One more interesting example of cut before we go: You might have noticed that the first character of the ls -l output is a d when it’s a directory and a – when it’s just a regular file.

Another useful flag for cut is -c, which lets you indicate specific character locations to use as the start location (or the start and end locations). For Western languages (which internationalization folk call this “Latin-1” languages, including Spanish, German, and Italian), one character = one letter, but in other, so called double-byte languages (Chinese, Arabic), a character doesn’t have quite the same meaning. For now you can ignore this nuance.

If we put those two flags together, we can use cut to answer the question “How many files and how many directories are in the current location?” This is a relatively complex pipe that summarizes how many of each suffix are found in a given ls -l output:

Click here to view code image

```
$ ls -l | awk 'NF > 2' | cut -c1 | sort | uniq -c
  15 -
  12 d
$
```

The awk weeds out all lines that don’t have at least three fields. (Remember the “Total” line we had to deal with earlier? Yeah, it’s again something we need to omit from our analysis.) Then cut slices just the first character of output, and then we simply sort and uniq it, and voila! We see that we have 15 plain files and 12 directories in the test directory.

The `cut` command has a very narrow set of capabilities, but when you’re extracting specific columns of information, either by field value or by counting characters, it’s a winner and worth knowing.

Don’t stop here, though. Read `man cut` for more details on how to work with this useful program.

## Inline Editing with sed and tr

Before we leave the topic of UNIX pipeline power tools, you need to learn about two more programs that are designed to change information as it goes through the data stream. The `sed` command, the more common of the two, is used primarily to substitute one pattern for another as information goes past. The `tr` command is even more limited: It translates one set of characters to another (but there are some surprising capabilities hidden in this otherwise dull utility).

## Action 9.3: Inline Editing with sed and tr

To more fully understand how each of these commands work, it’s useful to see them in action.

- 1. A common task for a pipeline is to change all uppercase letters into lowercase or vice versa. There are a number of ways to accomplish this within the Unix world, but the `tr` command makes it very easy:

![](img/036fe100817eada43c999b050270081b_172_0.png)

```
$ cut -d: -f5 /etc/passwd | tr '[a-z]' '[A-Z]' | tail
GREGORY SMITH
GORDON WILKINSON
THE RORT'N ONE
DAN KAMINSKY
EDWARD FULLER
HUMAN RIGHTS WEB
DAVID HELLER
JAIMIE MC CURRY
UNPRIVILEGED USER
$
```

The `tr` command does a 1:1 matching of what’s specified in the first argument with what’s specified in the second argument. In this case, you can see two ranges specified (`tr '[a-z]' '[A-Z]'`): all lowercase letters and then all uppercase letters.

If you’re working in multiple languages, a more sophisticated approach is to reference one of `tr`’s built-in character sets. Instead of using `'[a-z]'`, for example, use `'[:lower:]'`, which will work with Spanish, German, or whatever other language you or another user might be working with on the system.

[Table 9.1](#) lists the character sets that `tr` knows. It’s worth dog-earing this particular page so you can find it again later.
