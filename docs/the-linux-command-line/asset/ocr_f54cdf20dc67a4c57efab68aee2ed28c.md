# 23 — Printing

**Table 23-1: Common `pr` Options**

| Option | Description |
|---|---|
| `+first[:last]` | Output a range of pages starting with *first* and, optionally, ending with *last*. |
| `-columns` | Organize the content of the page into the number of columns specified by *columns*. |
| `-a` | By default, multi-column output is listed vertically. By adding the -a (across) option, content is listed horizontally. |
| `-d` | Double-space output. |
| `-D “format”` | Format the date displayed in page headers using *format*. See the man page for the date command for a description of the format string. |
| `-f` | Use form feeds rather than carriage returns to separate pages. |
| `-h “header”` | In the center portion of the page header, use *header* rather than the name of the file being processed. |
| `-l length` | Set page length to *length*. Default is 66 (US letter at 6 lines per inch) |
| `-n` | Number lines. |
| `-o offset` | Create a left margin *offset* characters wide. |
| `-w width` | Set page width to *width*. Default is 72. |

`pr` is often used in pipelines as a filter. In this example, we will produce a directory listing of `/usr/bin` and format it into paginated three-column output using `pr`:

```
```text
[me@linuxbox ~]$ ls /usr/bin | pr -3 -w 65 | head

2009-02-18 14:00                                      Page 1

[
411toppm                 apturl                 bsd-write
a2p                     ar                     bsh
a2ps                    arecord                 btflash
a2ps-lpr-wrapper        ark                    bug-buddy
```
```