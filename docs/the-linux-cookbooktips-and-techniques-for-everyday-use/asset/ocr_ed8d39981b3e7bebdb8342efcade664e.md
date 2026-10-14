# The Linux Cookbook: Tips and Techniques for Everyday Use:

```
$ pr -d -t term-paper 62; term-paper.print RET
```

To send the output directly to the printer for printing, you would pipe the output to lpr:

```
$ pr -d -t term-paper | lpr RET
```

NOTE: The pr ("print") tool is a text pre-formatter, often used to paginate and otherwise prepare text files for printing; there is more discussion on the use of this tool in Paginating Text.

# 14.1.4 Triple-Spacing Text

To triple-space text, where two blank lines are inserted between each line of the original text, use sed with the ' 'G;G' ' expression.

+   - To triple-space the file `term-paper` and write the output to the file `term-paper.print`, type:

```
$ sed 'G;G' term-paper 62; term-paper.print RET
```

The `G` expression appends one blank line to each line of sed's output; using `;` you can specify more than one blank line to append (but you must quote this command, because the semicolon (`;`) has meaning to the shell---see Passing Special Characters to Commands). You can use multiple `G` characters to output text with more than double or triple spaces.

+   - To quadruple-space the file `term-paper`, and write the output to the file `term-paper.print`, type:

```
$ sed 'G;G;G' term-paper 62; term-paper.print RET
```

The usage of sed is described in Editing Streams of Text.

# 14.1.5 Adding Line Breaks to Text

Sometimes a file will not have line breaks at the end of each line (this commonly happens during file conversions between operating systems). To add line breaks to a file that does not have them, use the text