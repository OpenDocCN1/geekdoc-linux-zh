# Appendix A

# A.1 Filters: An Introduction

A *filter* is a program that gets its input from the standard input (`stdin`), transforms it, and sends the transformed input to the standard output (`stdout`). The data passes “through” the filter, which typically has command-line options that control its behavior. A filter may also perform a “null” transformation, making no change at all to its input (which is what `cat` does.) Filters process text only, either from input files or from the output end of another Unix command (i.e., through a *pipe*.) All filters can be given optional filename arguments, in which case they take their input from the named files rather than from standard input. For example, in the command

```
$ cat first second third > combinedfile
```

`cat` reads files `first`, `second`, and `third` in that order and concatenates their contents, sending them to the standard output, which has been redirected to a file named `combinedfile`.

The most useful filters are

+   - `cut` (usually System V only) simple text cutting
+   - `grep` simple regular expressions as filtering pattern
+   - `egrep` extended (more powerful) regular expressions as filtering patterns
+   - `fgrep` fast, string matching expressions with alternation as patterns
+   - `sed` line-oriented text editing filter
+   - `awk` pattern-matching, field-oriented filter and full-fledged Turing computable programming language
+   - `cat` primitive filter with little transformation
+   - `sort` very general sorting filter
+   - `head,tail` lets only the top or bottom of a stream pass through
+   - `fold` wraps each input line to fit in a specified width

If your time is limited and you could learn but one of these, the most important would be `grep` – the return on your investment will be greatest. Coming in second would be `sed`, and then `awk`. The remaining filters are easy to learn and use and are described briefly first.

# A.1.1 sort

`sort` is easy to use:

```
$ sort file
```