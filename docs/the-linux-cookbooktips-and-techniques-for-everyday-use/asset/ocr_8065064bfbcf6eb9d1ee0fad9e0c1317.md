# 16.4.3 Processing LaTeX Files

The latex tool works just like tex, but is used to process LaTeX files.

+   - To process the LaTeX file `lshort.tex`, type:

```
$ latex lshort.tex RET
```

This command writes a DVI output file called `lshort.dvi`.

You may need to run latex on a file several times consecutively. LaTeX documents sometimes have indices and cross references, which, because of the way that LaTeX works, take two (and in rare cases three or more) runs through latex to be fully processed. Should you need to run latex through a file more than once in order to generate the proper references, you'll see a message in the latex processing output after you process it the first time instructing you to process it again.

+   - To ensure that all of the cross references in `lshort.tex` have been generated properly, run the input file through latex once more:

```
$ latex lshort.tex RET
```

The `lshort.dvi` file will be rewritten with an updated version containing the proper page numbers in the cross reference and index entries. You can then view, print, or convert this DVI file as described in the previous recipe for processing TeX files.

+   - To process the file `gentle.tex`, type:

```
$ tex gentle.tex RET
```

Once you have produced a DVI output file with this method, you can do the following with it:

+   - Preview it on the screen with xdvi; see Previewing a DVI File
+   - Print it with dvips or lpr; see Printing with Dvips
+   - Convert it to PostScript with dvips; see Preparing a DVI File for Printing; (then, you can also convert the PostScript output to PDF or plain text)