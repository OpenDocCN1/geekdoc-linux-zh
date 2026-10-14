The nl program is a rather arcane tool used to perform a simple task. It numbers lines. In its simplest use, it resembles cat -n.

```
[me@linuxbox ~]$ nl distros.txt | head
1  SUSE      10.2  12/07/2006
2  Fedora    10    11/25/2008
3  SUSE      11.0  06/19/2008
4  Ubuntu    8.04  04/24/2008
5  Fedora    8     11/08/2007
6  SUSE      10.3  10/04/2007
7  Ubuntu    6.10  10/26/2006
8  Fedora    7     05/31/2007
9  Ubuntu    7.10  10/18/2007
10 Ubuntu    7.04  04/19/2007
```

Like cat, nl can accept either multiple files as command line arguments or standard input. However, nl has a number of options and supports a primitive form of markup to allow more complex kinds of numbering.

nl supports a concept called logical pages when numbering. This allows nl to reset (start over) the numerical sequence when numbering. Using options, it is possible to set the starting number to a specific value and, to a limited extent, its format. A logical page is further broken down into a header, body, and footer. Within each of these sections, line numbering may be reset and/or be assigned a different style. If nl is given multiple files, it treats them as a single stream of text. Sections in the text stream are indicated by the presence of some rather odd-looking markup added to the text, as described in Table 21-1.

# Table 21-1: nl Markup

| Markup | Meaning |
|---|---|
| \:\\:\ | Start of logical page header |
| \:\ | Start of logical page body |
| \: | Start of logical page footer |

Each of the markup elements listed in Table 21-1 must appear alone on its own line. After processing a markup element, nl deletes it from