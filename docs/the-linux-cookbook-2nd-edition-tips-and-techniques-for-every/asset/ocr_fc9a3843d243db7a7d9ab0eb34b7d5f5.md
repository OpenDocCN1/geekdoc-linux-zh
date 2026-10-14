# 8.3.6 Finding the Percentage Two Files Differ By

Wdiff

DEB: wdiff
RPM: wdiff
WWW: http://www.gnu.org/software/wdiff/wdiff.html

The wdiff tool is a front-end to diff. It finds and displays the differences between words in the two text files you give as arguments. It outputs an annotated version of the second file, showing the changes necessary to make it identical to the first: Word deletions are marked like "[- this -]," additions are marked like "[+ this +]," and changes are marked like "{+ this +}."

⇒ To peruse an annotated copy of the file story_draft.1, showing the changes necessary to make it identical to the file story_draft.2, type:

```
$ wdiff story_draft.2 story_draft.1 | less RET
```

To forgo the default annotations and instead make annotations good for sending to a printer, use the -p option; deleted text is underlined and inserted text is output in bold.

⇒ Here are two ways to use this.

+   - To print an annotated copy of the file story_draft.1, showing the changes necessary to make it identical to the file story_draft.2, type:
+     $ wdiff -p story_draft.2 story_draft.1 | lpr RET

+   - To peruse an annotated copy of the file story_draft.1, showing the changes necessary to make it identical to the file story_draft.2 with underlining and bold lettering, type:
+     $ wdiff -p story_draft.2 story_draft.1 | less RET

Use wdiff with the -s option to display a number of statistics about the differences: the total number of words; the number of common words and the percentage relative to the total; the number of words deleted or inserted, and the percentage relative to the total; and the number of words changed, and the percentage relative to the total. These statistics are output as two lines at the end, after an annotation of the second file is output.