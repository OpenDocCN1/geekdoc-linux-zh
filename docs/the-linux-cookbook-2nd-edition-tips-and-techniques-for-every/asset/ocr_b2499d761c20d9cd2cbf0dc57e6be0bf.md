documents. (LaTeX probably gets more day-to-day use than the plain TeX format, but in my experience, each is useful for different situations.)

"TeX" isn't pronounced like the name of a cowboy, nor is "LaTeX" like a kind of paint: the letters "T," "E," and "X" represent the Greek characters tau, epsilon, and chi (from the Greek techne, meaning "art and science"). So the last sound in "TeX" is like the last sound in "Bach," and "LaTeX," depending on local dialect, is pronounced either "lay-tek" or "lah-tek." Those who become highly adept at using the system Knuth calls TeXnicians.

The collective family of TeX and related programs (including Metafont; see Recipe 16.5 [Using Other Font Tools], page 403) are sometimes called "TeX and friends," and they are always kept in a directory named texmf. For example, the supplementary files included with the bare TeX system are kept in the /usr/lib/texmf directory tree.

The following recipes describe how to begin writing input for TeX and how to process these files for viewing and printing. While not everyone wants or even needs to write documents with TeX and LaTeX, these formats are widely used—especially on Linux systems—so every Linux user has the potential to encounter one of these files, and ought to know how to process them.

# 15.3.1 Distinguishing Between TeX and LaTeX Files

There are separate commands for processing TeX and LaTeX files, and they're not interchangeable, so when you want to process a TeX or LaTeX input file, you should first determine its format.

By convention, TeX files always have a .tex file name extension. LaTeX input files sometimes have a .latex or .ltx file name extension instead, but not always—one way to tell if a .tex file is actually in the LaTeX format is to use grep to search the file for the text "\document," which every LaTeX (and not TeX) document will have. So if the search outputs any lines that match, you have a LaTeX file. (The regular expression to use with grep is "\document," because backslash characters must be specified with two backslashes.)

⇒ To determine whether the file smith.tex is a TeX or LaTeX file, type:

```
$ grep '\document' smith.tex [RET]
\documentclassletter
$
```