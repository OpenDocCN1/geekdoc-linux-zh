# INTRODUCTION 591

you can use the command Alt+X validate-tex-buffer to carry out a syntax check. Although Emacs sometimes signals errors when there are none, it will find most of the missing brackets.

While processing text, LaTeX issues not only error messages, but also warnings. Warnings do not interrupt the translation process. Many warnings begin with a message such as 'overfull hbox' and suggest that LaTeX has problems with line or page breaking. In many of these cases, manual intervention is required (suggested hyphenation, forced page breaks, and so on). These problems are described on page 618 onward.

The interactive behavior of LaTeX - that is, an interruption for each and every error - can be irritating, especially if the translation is to be automated. If you insert batchmode at the beginning of the LaTeX file, LaTeX no longer stops at errors (as you had entered Q at the occurrence of the first error). After the translation is finished, you can take your time to read through the log file.

While LaTeX is waiting for keyboard input, it does not react to Ctrl+C if you want to terminate the program during an input, you must press Ctrl+D (for end of file!). This emergency is particularly useful when LaTeX has encountered a wrong file name and you want to specify a different one. An alternative solution is to use null. Then, LaTeX loads the empty file null.sty which has been inserted into the LaTeX directory structure specifically for this purpose.

In your Linux distribution you will keep finding *.files which contain documentation for various programs. If large numbers of mysterious error messages occur when translating such files with LaTeX, the cause is usually that the file is not a LaTeX file but a tex file. Tex files have the extension *.tex, but they must be translated with tex file.

# Introductory example

Before the next section provides a systematic description of the most important LaTeX commands, the following example is intended to illustrate the general usage of LaTeX. After their translation, the LaTeX instructions listed below result in the page shown in Figure 18.1. For a longer article, it would obviously make more sense to print the contents list on a separate page and to the whole article with a title page – we had to do without this for reasons of space.

```
\documentclass[twocolumn,11pt]{article} % type: two-column article
\usepackage{isolatin} % ISO Latin character set

\parindent % no first line indent
\parskip % space between paragraphs
\columnsep % 1 cm gutter between columns
```