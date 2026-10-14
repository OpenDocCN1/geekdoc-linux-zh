
section to standard output. It can accept multiple file arguments or input from standard input.

Specifying the section of the line to be extracted is somewhat awkward and is specified using the following options:

## Table 20-3: cut Selection Options

| Option | Description |
|---|---|
| -c char_list | Extract the portion of the line defined by char_list. The list may consist of one or more comma-separated numerical ranges. |
| -f field_list | Extract one or more fields from the line as defined by field_list. The list may contain one or more fields or field ranges separated by commas. |
| -d delim_char | When -f is specified, use delim_char as the field delimiting character. By default, fields must be separated by a single tab character. |
| --complement | Extract the entire line of text, except for those portions specified by -c and/or -f. |

As we can see, the way cut extracts text is rather inflexible. cut is best used to extract text from files that are produced by other programs, rather than text directly typed by humans. We’ll take a look at our distros.txt file to see if it is “clean” enough to be a good specimen for our cut examples. If we use cat with the -A option, we can see if the file meets our requirements of tab-separated fields:

```
[me@linuxbox ~]$ cat -A distros.txt
SUSE^I10.2^I12/07/2006$
Fedora^I10^I11/25/2008$
SUSE^I11.0^I06/19/2008$
Ubuntu^I8.04^I04/24/2008$
Fedora^I8^I11/08/2007$
SUSE^I10.3^I10/04/2007$
Ubuntu^I6.10^I10/26/2006$
Fedora^I7^I05/31/2007$
Ubuntu^I7.10^I10/18/2007$
Ubuntu^I7.04^I04/19/2007$
SUSE^I10.1^I05/11/2006$
Fedora^I6^I10/24/2006$
Fedora^I9^I05/13/2008$
```

```
Ubuntu^I6.06^I06/01/2006$
Ubuntu^I8.10^I10/30/2008$
Fedora^I5^I03/20/2006$
```

It looks good. No embedded spaces, just single tab characters between the fields. Since the file uses tabs rather than spaces, we’ll use the -f option to extract a field:

```
[me@linuxbox ~]$ cut -f 3 distros.txt
12/07/2006
11/25/2008
06/19/2008
04/24/2008
11/08/2007
10/04/2007
10/26/2006
05/31/2007
10/18/2007
04/19/2007
05/11/2006
10/24/2006
05/13/2008
06/01/2006
10/30/2008
03/20/2006
```

Because our distros file is tab-delimited, it is best to use cut to extract fields rather than characters. This is because when a file is tab-delimited, it is unlikely that each line will contain the same number of characters, which makes calculating character positions within the line difficult or impossible. In our example above, however, we now have extracted a field that luckily contains data of identical length, so we can show how character extraction works by extracting the year from each line:

```
[me@linuxbox ~]$ cut -f 3 distros.txt | cut -c 7-10
2006
2008
2008
2008
2007
2007
2006
2007
2007
2007
2006
2006
2008
2006
2008
2006
```

```
2006
2008
2006
2008
2006
```

By running cut a second time on our list, we are able to extract character positions 7 through 10, which corresponds to the year in our date field. The 7-10 notation is an example of a range. The cut man page contains a complete description of how ranges can be specified.

## Expanding Tabs

Our distros.txt file is ideally formatted for extracting fields using cut. But what if we wanted a file that could be fully manipulated with cut by characters, rather than fields? This would require us to replace the tab characters within the file with the corresponding number of spaces. Fortunately, the GNU Coreutils package includes a tool for that. Named expand, this program accepts either one or more file arguments or standard input, and outputs the modified text to standard output.

If we process our distros.txt file with expand, we can use the cut -c to extract any range of characters from the file. For example, we could use the following command to extract the year of release from our list, by expanding the file and using cut to extract every character from the twenty-third position to the end of the line:

```
[me@linuxbox ~]$ expand distros.txt | cut -c 23-
```

Coreutils also provides the unexpand program to substitute tabs for spaces.

When working with fields, it is possible to specify a different field delimiter rather than the tab character. Here we will extract the first field from the /etc/passwd file:

```
[me@linuxbox ~]$ cut -d ':' -f 1 /etc/passwd | head
root
daemon
bin
sys
sync
games
man
lp
```
