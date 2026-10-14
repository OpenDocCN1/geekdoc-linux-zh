In this example, grep returned a match, so it’s safe to assume that smith.tex is a LaTeX file (of the “letter” document class) and not a TeX file.

NOTES: For more on regular expressions and searching with grep, see Recipe 14.3 [Regular Expressions—Matching Text Patterns], page 335.

# 15.3.2 Processing a TeX File

Use tex to process TeX files. It takes as an argument the name of the TeX source file to process, and it writes an output file in DVI (“DeVice Independent”) format, with the same base file name as the source file, but with a .dvi extension.

⇒ To process the file gentle.tex, type:

```
$ tex gentle.tex [RET]
```

Once you have produced a DVI output file with this method, you can do any of the following with it:

+   - Preview it on the screen with xdvi; see Recipe 17.4.1 [Previewing a DVI File], page 413.
+   - Print it with dvips or lpr; see Recipe 25.2.5 [Printing a DVI File], page 515.
+   - Convert it to PostScript with dvips; see Recipe 25.3.2 [Preparing a DVI File for Printing], page 520; then, you can also convert the PostScript output to PDF or plain text.

# 15.3.3 Processing a LaTeX File

The latex tool works just like tex, but it is used to process LaTeX files.

⇒ To process the LaTeX file lshort.tex, type:

```
$ latex lshort.tex [RET]
```

This command writes a DVI output file called lshort.dvi.

You may need to run latex on a file several times consecutively. LaTeX documents sometimes have indices and cross references, which, because of the way that LaTeX works, take two (and, in rare cases, three or more) runs through latex to be fully processed. Should you need to run a file through latex more than once in order to generate the proper references, you’ll see a message in the latex processing output instructing you to process it again.