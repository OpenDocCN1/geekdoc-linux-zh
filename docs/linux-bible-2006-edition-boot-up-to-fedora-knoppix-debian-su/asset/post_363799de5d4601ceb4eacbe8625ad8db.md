
Most pages are stored in subdirectories of /usr/share/man. Before you create a man page, refer to similar man pages to see the markup and the headings they include. man1 has commands; man2 has system calls; man3 has library functions; man4 has special devices (/dev/*); man5 has file formats; man6 has games; man7 has miscellaneous components; man8 has administrative commands.

A few other macros are used in the man page. The .IP format indented paragraphs for things like options. The man page also contains lower-level font requests; for example, \B says to change the current font to bold, \I changes the font to italic, and \R changes it back to regular font. (This markup is better than asking for a particular font type because it changes to bold, italic, or regular for the current font.) Figure 21-4 shows what the man page page looks like if it is formatted with groff:

```
$ groff -man -T waycool.1
```

| man(1) | waycool(1) |
|---|---|
| NAME | waycool - any cool command |
| SYNOPSIS | waycool [options] [file, ... ] |
| VERSION | This man page documents the GNU waycool command. This version of waycool is better than the last one. |
| DESCRIPTION | waycool is a cool command. |
| OPTIONS | -b display with bold. |
| -i display with italic. |
| -a affect symbols like indent available only on systems that can change the alignment. |
| -v print the version number with the command. |
| COMMAND | If you don't like the command, don't use it. It will just hurt your fingers. |
| ENVIRONMENT VARIABLES | These variables are used by waycool. |
| DISPLAY | this contains the display. |
| WAYCOOL | this contains the location of the waycool datastore. |
| FILES | /var/waycool - directory containing waycool staff. |
| AUTHOR | Chuck Bird <cbird@example.com> |
| REPORTING BUGS | Report bugs to bugs@example.com |
| COPYRIGHT | (C) 2003 Free Software Foundation, Inc. This software is distributed as-is without any copying conditions. There is NO WARRANTY, not ANY KIND, LIABILITY OR FITNESS FOR A PARTICULAR PURPOSE |
| ACKNOWLEDGMENTS | I'd like to thank all friends. |

Figure 21-4: Man page formatting adds headers and lays out the page of text.

Table 21-1 lists the macros that you can use on your man pages. These macros are described on the man(7) manual page (type man 7 man to view that page).

## Table 21-1: Man Macros

| Macro | Description |
|---|---|
| .B | Bold. |
| .BI | Bold, then italics (alternating). |
| .BR | Bold, then Roman (alternating). |
| .DT | Set default tabs. |
| .HP | Begin a hanging indent. |
| .I | Italics. |
| .IB | Italics, then bold (alternating). |
| .IP | Begin hanging tag. For options use .TP. |
| .IR | Italics, then Roman (alternating). |
| .LP | Begin paragraph. |
| .PD | Set distance between paragraphs. |
| .PP | Begin paragraph. |
| .RB | Roman, then bold (alternating). |
| .RE | End relative indent (after .RS). |
| .RI | Roman, then italics (alternating). |
| .RS | Begin relative indent (use .RE to end indent). |
| .SB | Small text, then bold (alternating). |
| .SM | Small text. Used to show words in all caps. |
| .SH | Section head. |
| .SS | Subheading within a .SH heading. |
| .TH | Title heading. Used once at the beginning of the man page. |
| .TP | Begin a hanging tag. Begins text on next line, not same line as tag. |

## Creating a Letter, Memo, or White Paper with Groff

Memorandum macros (which are used with the -mm option of groff) were once popular among UNIX users for producing technical documents, letters, and memos. Although modern word processors with a variety of WYSIWYG templates have made mm macros outdated, in a pinch they are still a quick way to create a typeset-style document in a text environment.

To format and print (to a PostScript printer) a document with mm macros, use the following:

```
$ groff -mm -Tps -1 letter.mm
```

Here's a simple example of how to use mm macros to produce a letter:

```
.WA "Christopher T. Craft"
999 Anyway Way
Anytown, UT 84111 USA
.WE
.IA
John W. Doe
111 Notown Blvd.
Notown, UT 84111
.IE
.LO RN "Our telephone conversation"
.LO SA "Dear Mr. Doe:"
.LT
In reference to our telephone conversation on the 4th. I am calling to confirm our upcoming appointment on the 18th. I look forward to discussing the merger. I believe we have a win-win situation here.
.FC "Yours Truly,"
.SG
```

Use the following command to format the document and save the output to a named letter.ps:

```
$ groff -mm -Tps -1 letter.mm > letter.ps
```

The output will look like Figure 21-5.

> If you get from the groff command that says letter.mm:15: warning 'let*wa-titlell' not defined, you can safely disregard it. Alternatively, add a set of empty double quotes to the end of the first line. That is, change the first line of letter.mm to read

```
.WA "Christopher T. Craft" ""
```

## Chapter 21: Working with Words and Images 561

![](img/a2d958d7eab32ca5b89b2b8af808aa70_592_0.png)

Figure 21-5: Create a simple letter using mm macros.

The mm macros were often used to produce technical memos. The following is an example of a sign-off memo that might go at the front of a larger technical memo:

+   . TL
Merger Technical Specifications
.AF "ABC Corporation"
.AU "Christopher Craft"
.AT "President"
.AS
This memo details the specifications for the planned merger.
.AE
.MT "Merger Description and Marching Orders"
As a result of our talks with XYZ corporation, we plan to go forward with the merger. This document contains the following:
.BL
.LI
Schedule and time tables.
.LI
Financial statements.
.LI
Asset allocations.
.LE
.SP
Please add any corrections you have, then sign the approval line indicated at the bottom of this sheet.

+   . FC
. SG
.AV "John W. Doe, XYZ Corporation President"
.AV "Sylvia Q. Public, XYZ Corporation CFO"
.NS
Everyone in the corporation.
. NE

Figure 21-6 shows the output of this memo.

![](img/a2d958d7eab32ca5b89b2b8af808aa70_593_0.png)

Figure 21-6: Adding headings and approval lines automatically to memos.

> Note
For a complete listing of mm macros, see the groff_mm man page.

## Part IV: Running Applications 562

## Chapter 21: Working with Words and Images 563

### Adding Equations, Tables, and Pictures

To create a table in a Groff document, use the .TS and .TE macros. The following is an example of the markup used to produce a simple table:

```
.TS
center, box, tab(:);
cs s
c | c | c
| 1.
Mergers and Acquisitions Team
=
Employee:Title:Location
Jones, James:Manager:New York Office
Smith, Charles:Sales Manager:Los Angeles Office
Taylor, Sarah:R&D Manager:New York Office
Walters, Mark:Information Systems Manager:Salt City
```

The .TS macro starts the table, and the line indicates that the table should be centered (center) and surrounded by a line box and a colon (Tab(:)). The third line shows that the header should be centered in the box (|) and span across the cells (s). The fourth line shows that the header of each cell should be centered (| c | c) and the fifth line indicates that the data cells that follow should be justified (| l | l |).

> There must be a period at the end of the table definition line. In this example, after the | | | line. If the period is not there, tbl tries to interpret the text as of table definition, fails, and stops the table; the does not print.

The rest of the information in the table is the data. Note that the table separators are colon characters (:). End the table with a .TE macro. If the table were a memo called memotbl.mm, tbl could process the memo and send it to the printer using the following:

```
$ groff -Tps -1 -mm -t memotbl.mm
```

Data between .TS and .TE macros are interpreted as tables. Figure 21-7 displays the output from this example.

![](img/a2d958d7eab32ca5b89b2b8af80aa70_594_0.png)

Figure 21-7: How to set text justified with the use of the tbl command .TS and .TE macros.
