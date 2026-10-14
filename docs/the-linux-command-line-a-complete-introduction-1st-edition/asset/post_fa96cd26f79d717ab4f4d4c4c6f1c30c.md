
# 21

# FORMATTING OUTPUT

In this chapter, we continue our look at text-related tools, focusing on programs that are used to format text output rather than change the text itself. These tools are often used to prepare text for printing, a subject that we will cover in the next chapter. The programs that we will cover in this chapter include the following:

+   - nl—Number lines.
+   - fold—Wrap each line to a specified length.
+   - fmt—A simple text formatter.
+   - pr—Format text for printing.
+   - printf—Format and print data.
+   - groff—A document formatting system.

## Simple Formatting Tools

We’ll look at some of the simple formatting tools first. These are mostly single-purpose programs, and a bit unsophisticated in what they do, but they can be used for small tasks and as parts of pipelines and scripts.

### nl—Number Lines

The nl program is a rather arcane tool used to perform a simple task: It numbers lines. In its simplest use, it resembles cat -n:

```
[me@linuxbox ~]$ nl distros.txt | head
1  SUSE        10.2   12/07/2006
2  Fedora      10     11/25/2008
3  SUSE        11.0   06/19/2008
4  Ubuntu      8.04   04/24/2008
5  Fedora      8      11/08/2007
6  SUSE        10.3   10/04/2007
7  Ubuntu      6.10   10/26/2006
8  Fedora      7      05/31/2007
9  Ubuntu      7.10   10/18/2007
10 Ubuntu      7.04   04/19/2007
```

Like cat, nl can accept either multiple filenames as command-line arguments or standard input. However, nl has a number of options and supports a primitive form of markup to allow more complex kinds of numbering.

nl supports a concept called logical pages when numbering. This allows nl to reset (start over) the numerical sequence when numbering. Using options, it is possible to set the starting number to a specific value and, to a limited extent, set its format. A logical page is further broken down into a header, body, and footer. Within each of these sections, line numbering may be reset and/or be assigned a different style. If nl is given multiple files, it treats them as a single stream of text. Sections in the text stream are indicated by the presence of some rather odd-looking markup added to the text, as shown in Table 21-1.

### Table 21-1: nl Markup

| Markup | Meaning |
|---|---|
| \:\\:\\: | Start of logical-page header |
| \:\\: | Start of logical-page body |
| \: | Start of logical-page footer |

Each of the markup elements in Table 21-1 must appear alone on its own line. After processing a markup element, nl deletes it from the text stream.

### Table 21-2: Common nl Options

| Option | Meaning |
|---|---|
| -b style | Set body numbering to style, where style is one of the following:
- a Number all lines.
- t Number only non-blank lines. This is the default.
- n None.
- pregexp Number only lines matching basic regular expression regexp. |
| -f style | Set footer numbering to style. Default is n (none). |
| -h style | Set header numbering to style. Default is n (none). |
| -i number | Set page numbering increment to number. Default is 1. |
| -n format | Set numbering format to format, where format is one of the following:
- ln Left justified, without leading zeros.
- rn Right justified, without leading zeros. This is the default.
- rz Right justified, with leading zeros. |
| -p | Do not reset page numbering at the beginning of each logical page. |
| -s string | Add string to the end of each line number to create a separator. Default is a single tab character. |
| -v number | Set first line number of each logical page to number. Default is 1. |
| -w width | Set width of the line number field to width. Default is 6. |

Admittedly, we probably won’t be numbering lines that often, but we can use nl to look at how we can combine multiple tools to perform more complex tasks. We will build on our work in the previous chapter to produce a Linux distributions report. Since we will be using nl, it will be useful to include its header/body/footer markup. To do this, we will add it to the sed script from the last chapter. Using our text editor, we will change the script as follows and save it as distros-nl.sed:

```
# sed script to produce Linux distributions report

1 !
\\:\\:\\:\\
\
Linux Distributions Report\
\
Name            Ver.    Released
----            ---     -------
\\:\\1:
s/[[0-9]\{2\}\/\([0-9]\{2\}\)\/\([0-9]\{4\}\)/$\3-\1-\2/
```
