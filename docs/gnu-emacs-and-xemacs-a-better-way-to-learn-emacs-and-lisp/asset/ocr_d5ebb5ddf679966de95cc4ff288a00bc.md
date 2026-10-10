Another second-level section, but still a part of the top-level Section 1.

*** Part 1

A third-level header, this one belonging to Sub-section 2.

* Section 2

The second top-level subdivision of the document.

If this example were to be collapsed, it would look like this:

+   - Section 1 ...
+   - Sub-section 1 ...
+   - Sub-section 2 ...
+   - Part 1 ...
+   - Section 2 ...

It isn't absolutely necessary to use the default asterisks as section-level indicators. A variable called \emph{outline-regexp} can be changed to correspond to heading levels of a particular type of document. The default value is \verb|(^\\\\L)|, which can be translated as ``one or more of either *- or the control character ^L, a single character that is used to indicate page boundaries''. A built-in limitation of \textsc{Outline} mode is that the higher the level, the shorter the level indicators must be. You can get around this by using just part of a word indicator, a part shorter than the next-lower indicator in the hierarchy. An example will clarify this. Suppose you were editing documents that used (in descending order) the levels Part, Chapter, and Scene. Part is a short word, but the word Scene is shorter than Chapter and longer than Part. Chapter is the one level indicator that doesn't follow the ``lower level requires a longer name'' rule, so Chapter needs to be truncated to fit the rule. A problem arises: if Chapter is shortened to Chapt to make it longer than Part, it ends up the same length as Scene. There is nothing to do here but add a character to Scene to make it longer. Using an asterisk as that character, the three strings for the new regular expression are Part, Chapt, and *Scene. Plugging these into a Lisp statement results in this:

```
(\\(Part\\|Chapt\\|^\\*Scene\\)\\*)
```

This is a complicated-looking regular expression. The numerous backslashes are necessary to ``escape'' the characters that otherwise would be interpreted as regular-expression special characters.