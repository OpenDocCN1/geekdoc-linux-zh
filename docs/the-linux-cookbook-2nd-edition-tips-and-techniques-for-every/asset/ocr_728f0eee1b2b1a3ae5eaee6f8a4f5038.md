⇒ To convert all of the `.DOC` Word files in the current directory to \LaTeX files with maximum line widths of 40 characters, type:

```
$ word2x -f latex -w 40 *.DOC [RET]
```

# 26.5.2 Converting Word to Plain Text

To convert a Word file to plain text, use word2x and give “text” as an argument to the -format option.

⇒ To convert the Word file resume.doc to a plain text file called resume, type:

```
$ word2x -f text resume.doc resume [RET]
```

To send a conversion to the standard output, give a hyphen character (-) as the output file to use. This is useful for piping the plain text conversion to other tools that work on text, such as grep, a tool for searching text (see Recipe 14.1 [Searching Text for a Word], page 333).

⇒ To search the text of the Word file resume.doc for the string “linux,” regardless of case, type:

```
$ word2x resume.doc - | grep -i linux [RET]
```

These commands convert the Word file resume.doc to text and output all lines of that text, if any, that contain the string “linux” regardless of case. The original resume.doc file is unaltered.

# 26.6 Converting Text from Proprietary Formats

Use Recipe 9.3.6 [Listing Text in Binary Files], page 228, to output any text strings saved in a file with a proprietary format. This does not always work because not all proprietary formats keep text in ASCII strings, but it’s usually worth trying.

⇒ To peruse all of the ASCII strings in the file HCX1010A.BIN, type:

```
$ strings HCX1010A.BIN | less [RET]
```

# 26.7 Managing ZIP Archives

Unzip
DEB: unzip
RPM: unzip
WWW: http://www.info-zip.org/