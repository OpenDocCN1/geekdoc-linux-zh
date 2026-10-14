
Now we see that the editing is not carried out, because our input stream does not have a line 2.

Addresses may be expressed in many ways. Table 20-7 lists the most common ones.

## Table 20-7: sed Address Notation

| Address | Description |
|---|---|
| n | A line number where n is a positive integer |
| $ | The last line |
| /regexp/ | Lines matching a POSIX basic regular expression. Note that the regular expression is delimited by slash characters. Optionally, the regular expression may be delimited by an alternate character, by specifying the expression with \cregexpc, where c is the alternate character. |
| addr1,addr2 | A range of lines from addr1 to addr2, inclusive. Addresses may be any of the single address forms above. |
| first~step | Match the line represented by the number first and then each subsequent line at step intervals. For example, 1~2 refers to each odd-numbered line, and 5~5 refers to the fifth line and every fifth line thereafter. |
| addr1,+n | Match addr1 and the following n lines. |
| addr2! | Match all lines except addr2, which may be any of the forms above. |

We’ll demonstrate different kinds of addresses using the distros.txt file from earlier in this chapter. First, a range of line numbers:

```
[me@linuxbox ~]$ sed -n '1,5p' distros.txt
SUSE      10.2    12/07/2006
Fedora    10      11/25/2008
SUSE      11.0    06/19/2008
Ubuntu    8.04    04/24/2008
Fedora    8       11/08/2007
```

In this example, we print a range of lines, starting with line 1 and continuing to line 5. To do this, we use the p command, which simply causes a matched line to be printed. For this to be effective, however, we must include the option -n (the no autoprint option) to cause sed not to print every line by default.

Next, we'll try a regular expression:

```
[me@linuxbox ~]$ sed -n '/SUSE/'p distros.txt
SUSE    10.2    12/07/2006
SUSE    11.0    06/19/2008
SUSE    10.3    10/04/2007
SUSE    10.1    05/11/2006
```

By including the slash-delimited regular expression /SUSE/, we are able to isolate the lines containing it in much the same manner as grep.

Finally, we'll try negation by adding an exclamation point (!) to the address:

```
[me@linuxbox ~]$ sed -n '/SUSE/'!p distros.txt
Fedora  10    11/25/2008
Ubuntu  8.04  04/24/2008
Fedora  8     11/08/2007
Ubuntu  6.10  10/26/2006
Fedora  7     05/31/2007
Ubuntu  7.10  10/18/2007
Ubuntu  7.04  04/19/2007
Fedora  6     10/24/2006
Fedora  9     05/13/2008
Ubuntu  6.06  06/01/2006
Ubuntu  8.10  10/30/2008
Fedora  5     03/20/2006
```

Here we see the expected result: all of the lines in the file except the ones matched by the regular expression.

So far, we've looked at two of the sed editing commands, s and p.

## Table 20-8: sed Basic Editing Commands

| Command | Description |
|---|---|
| = | Output current line number. |
| a | Append text after the current line. |
| d | Delete the current line. |
| i | Insert text in front of the current line. |
| p | Print the current line. By default, sed prints every line and edits only lines that match a specified address within the file. The default behavior can be overridden by specifying the -n option. |
| q | Exit sed without processing any more lines. If the -n option is not specified, output the current line. |

## Table 20-8 *(continued)*

| Command | Description |
|---|---|
| `q` | Exit sed without processing any more lines. |
| `s/regexp/replacement/` | Substitute the contents of `replacement` wherever `regexp` is found. `replacement` may include the special character `&`, which is equivalent to the text matched by `regexp`. In addition, `replacement` may include the sequences `\1` through `\9`, which are the contents of the corresponding subexpressions in `regexp`. For more about this, see the following discussion on back references. After the trailing slash following `replacement`, an optional flag may be specified to modify the `s` command’s behavior. |
| `y/set1/set2` | Perform transliteration by converting characters from `set1` to the corresponding characters in `set2`. Note that unlike `tr`, `sed` requires that both sets be of the same length. |

The `s` command is by far the most commonly used editing command. We will demonstrate just some of its power by performing an edit on our `distros.txt` file. We discussed before how the date field in `distros.txt` was not in a “computer-friendly” format. While the date is formatted MM/DD/YYYY, it would be better (for ease of sorting) if the format were YYYY-MM-DD. To perform this change on the file by hand would be both time consuming and error prone, but with sed, this change can be performed in one step:

```
[me@linuxbox ~]$ sed 's/\([0-9]\{2\}\)\/\([0-9]\{2\}\)\/\([0-9]\{4\}\)$/\3-\1-\2/' distros.txt
SUSE        10.2    2006-12-07
Fedora      10      2008-11-25
SUSE        11.0    2008-06-19
Ubuntu      8.04    2008-04-24
Fedora      8       2007-11-08
SUSE        10.3    2007-10-04
Ubuntu      6.10    2006-10-26
Fedora      7       2007-05-31
Ubuntu      7.10    2007-10-18
Ubuntu      7.04    2007-04-19
SUSE        10.1    2006-05-11
Fedora      6       2006-10-24
Fedora      9       2008-05-13
Ubuntu      6.06    2006-06-01
Ubuntu      8.10    2008-10-30
Fedora      5       2006-03-20
```

Wow! Now that is an ugly-looking command. But it works. In just one step, we have changed the date format in our file. It is also a perfect example of why regular expressions are sometimes jokingly referred to as a “write-only”
