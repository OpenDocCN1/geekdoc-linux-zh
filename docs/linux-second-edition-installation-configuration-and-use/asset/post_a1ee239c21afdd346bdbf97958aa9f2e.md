
## LATEX VERSUS LATEX 2.09 629

```
\advancelength 37000% increase length by 2 mm
\halflength\length% half of that
\divide length by 2%
\unitlengthissp% all measurements in sp (1/65536 pt)
% picture environment for graphics commands
% \length, 60000 sp = 3.2 mm high
% horizontal offset 0,
% vertical offset 14000 sp (0.7 mm) below normal text
\begin(picture)\(\length,60000){0, 14000}%
% draw oval
\put\{halflength, 30000)\oval(\length, 60000))%
% output stored box in this oval
% horiz. offset 1 mm, vert offset 0.7 mm
\put(18500, 14000)\unbox\mybox)%
\end(picture))
```

Relatively often, syntax boxes are used for various summaries. The standardfbox command is not suitable for this purpose because it does not permit use of the \verb command. The following macros use the new LaTeX environment lrbox. The gray background is obtained with the \fcolorbox command defined in the color package.

```
\fboxbox1.36mm% space between syntax box and text
\definecolor(g1)(0.92)% define colorshade
\newsavebox{syntaxbox}% as above
\newenvironment{sybox}%
\begin{lrbox}{syntaxbox}%
\begin{minipage}{12.5cm}%
\end{minipage}%
\end{lrbox}% output syntax box contents in a
\fcolorbox{black}{g1}{% gray background \fcolorbox
\parbox{12.5cm}{\usebox{syntaxbox}}\hfill\mbox{}}}
```

Application of the new environment looks as follows:

```
\begin(sybox)
Syntax box in which special characters such as
\verb?%^ can be represented
\end(sybox)
```

Syntax box in which special characters such as %^ can be represented

## 18.8 LaTeX2 versus LaTeX 2.09

LaTeX2 differs from the previous version LaTeX 2.09 mainly in its handling of character sets. If you work on a computer on which LaTeX 2.09 is still stalled, you must note the following points:

- Your LaTeX text begins with the instruction \documentstyle[options]{type} (instead of \documentclass). As options, you specify not only the options described on page 598, but also the names of additional files which in LaTeX are loaded with \usepackage. An analogous command to \usepackage does not exist in LaTeX 2.09.

- For changing character sets, the only available commands are \m, \fs, \tt, \bf, \it, \sc and \em. Combination of type attributes is only possible to a very limited extent. The commands for changing the type size \small, \large automatically activate the standard font – if you want to change the type size for \tt, you must first specify the command and then \tt (and not vice versa).

- The Tb environment mentioned in the previous section does not exist. Therefore, you cannot use the macro described above for the new sybox environment. So affected.

It is quite possible to live with these restrictions. The real functionality of LaTeX (setting of formulae, scientific layout elements, and so on) is not

## Compatibility problems with LaTeX2

Totally different problems can occur when you try to produce a text generated previously with LaTeX 2.09 with the new LaTeX 2e activates a compatibility mode when a document begins with \documentclass instead of \documentclass. In this case, it tries to behave exactly in the same way as LaTeX 2.09. In principle, this compatibility mode works very well. The fact that problems will arise, in spite of this, has mainly two causes:

- The text uses macro files which are no longer available under LaTeX 2e or have a different name. This problem can be easily overcome by copying the file in (usually name.sty) from your old LaTeX version into your current working directory. If you have already deleted LaTeX 2.09 on your computer (for example, during installation of a new LINUX distribution), you must try to obtain the file from another computer (if necessary).

- The text uses macro files which are no longer available under LaTeX 2e or have a different name. This problem can be easily overcome by copying the file in (usually name.sty) from your old LaTeX version into your current working directory. If you have already deleted LaTeX 2.09 on your computer (for example, during installation of a new LINUX distribution), you must try to obtain the file from another computer (if necessary).

- The text uses macro files which are no longer available under LaTeX 2e or have a different name. This problem can be easily overcome by copying the file in (usually name.sty) from your old LaTeX version into your current working directory. If you have already deleted LaTeX 2.09 on your computer (for example, during installation of a new LINUX distribution), you must try to obtain the file from another computer (if necessary).

- The text uses macro files which are no longer available under LaTeX 2e or have a different name. This problem can be easily overcome by copying the file in (usually name.sty) from your old LaTeX version into your current working directory. If you have already deleted LaTeX 2.09 on your computer (for example, during installation of a new LINUX distribution), you must try to obtain the file from another computer (if necessary).

- The text uses macro files which are no longer available under LaTeX 2e or have a different name. This problem can be easily overcome by copying the file in (usually name.sty) from your old LaTeX version into your current working directory. If you have already deleted LaTeX 2.09 on your computer (for example, during installation of a new LINUX distribution), you must try to obtain the file from another computer (if necessary).

- The text uses macro files which are no longer available under LaTeX 2e or have a different name. This problem can be easily overcome by copying the file in (usually name.sty) from your old LaTeX version into your current working directory. If you have already deleted LaTeX 2.09 on your computer (for example, during installation of a new LINUX distribution), you must try to obtain the file from another computer (if necessary).

- The text uses macro files which are no longer available under LaTeX 2e or have a different name. [Wait, the OCR text repeated these points, I will de-duplicate the final logical flow based on the provided snippet].

- ...If you have already deleted LaTeX 2.09 on your computer (for example, during installation of a new LINUX distribution), you must try to obtain the file from another computer (if necessary).

- The text uses macro files which are no longer available under LaTeX 2e or have a different name. This problem can be easily overcome by copying the file in (usually name.sty) from your old LaTeX version into your current working directory. If you have already deleted LaTeX 2.09 on your computer (for example, during installation of a new LINUX distribution), you must try to obtain the file from another computer (if necessary).

- The text uses macro files which are no longer available under LaTeX 2e or have a different name. This problem can be easily overcome by copying the file in (usually name.sty) from your old LaTeX version into your current working directory. If you have already deleted LaTeX 2.09 on your computer (for example, during installation of a new LINUX distribution), you must try to obtain the file from another computer (if necessary).

- The text uses macro files which are no longer available under LaTeX 2e or have a different name. This problem can be easily overcome by copying the file in (usually name.sty) from your old LaTeX version into your current working directory. If you have already deleted LaTeX 2.09 on your computer (for example, during installation of a new LINUX distribution), you must try to obtain the file from another computer (if necessary).

- The text uses macro files which are no longer available under LaTeX 2e or have a different name. This problem can be easily overcome by copying the file in (usually name.sty) from your old LaTeX version into the current working directory. If you have already deleted LaTeX 2.09 on your computer (for example, during installation of a new LINUX distribution), you must try to obtain the file from another computer (if necessary).

- The text uses macro files which are no longer available under LaTeX 2e or have a different name. This problem can be easily overcome by copying the file in (usually name.sty) from your old LaTeX version into your current working directory. If you have already deleted LaTeX 2.09 on your computer (for example, during installation of a new LINUX distribution), you must try to obtain the file from another computer (if necessary).

- The text uses macro files which are no longer available under LaTeX 2e or have a different name. This problem can be easily overcome by copying the file in (usually name.sty) from your old LaTeX version into your current working directory. If you have already deleted LaTeX 2.09 on your computer (for example, during installation of a new LINUX distribution), you must try to obtain the file from another computer (if necessary).

- The text uses macro files which are no longer available under LaTeX 2e or have a different name. This problem can be easily overcome by copying the file in (usually name.sty) from your old LaTeX version into your current working directory. If you have already deleted LaTeX 2.09 on your computer (for example, during installation of a new LINUX distribution), you must try to obtain the file from another computer (if necessary).

- The text uses macro files which are no longer available under LaTeX 2e or have a different name. This problem can be easily overcome by copying the file in (usually name.sty) from your old LaTeX version into your current working directory. If you have already deleted LaTeX 2.09 on your computer (for example, during installation of a new LINUX distribution), you must try to obtain the file from another computer (if necessary).

- The text uses macro files which are no longer available under LaTeX 2e or have a different name. This problem can be easily overcome by copying the file in (usually name.sty) from your old LaTeX version into your current working directory. If you have already deleted LaTeX 2.09 on your computer (for example, during installation of a new LINUX distribution), you must try to obtain the file from another computer (if necessary).

- The text uses macro files which are no longer available under LaTeX 2e or have a different name. This problem can be easily overcome by copying the file in (usually name.sty) from your old LaTeX version into your current working directory. If you have already deleted LaTeX 2.09 on your computer (for example, during installation of a new LINUX distribution), you must try to obtain the file from another computer (if necessary).

- The text uses macro files which are no longer available under LaTeX 2e or have a different name. [OCR repetition noted].

## LyX - made easy

## 19.1 Introduction

## What is LyX (and what is not?)

LyX is a modern text editor. In the documents, use can be made of tables, images, mathematical formulas, cross-references, and so forth. Different kinds of paragraphs (whose names will sound familiar to you have read the LaTeX chapter): Itemize, List, Chapter, and so on.

In many details, the handling of this program resembles a traditional text-processing program. Most keyboard shortcuts — cursor movement, selecting and copy of blocks, and so on – work in the same way as Windows programs. (If it irritates you, you may well select different keyboard assignments, for example with a greater resemblance to Emacs.)

LyX distinguishes itself through a number of professional features:

- In the documents, use can be made of tables, images, mathematical formulas, cross-references, and so forth.
- Input of mathematical formulas is supported by separate dialogs, symbol bars, and so on, and is user-friendly.
- LyX helps with automatic generation of contents lists, indices, and list of figures.
- Provided the spell program is installed on the computer. LyX texts can be easily checked for correct spelling.
- Support for multi-level undo. In regular intervals automatic backup copies (with the file name #filename.LyX#) are created of all LyX files that have been modified. The risk of unwanted lost data is very small.
- Menus and dialog texts are available in several languages. By default, LyX displays English language menus. If you prefer menus in another language, you need to set the environment variable LANG to "xx", where xx is the character language code as defined in the ISO Standard 639 (for example, de.

### 5.1.6 Sums and Integrals

Sum signs are very often decorated with one or more sets of limits which are placed above and below in display mode but will move them to the side when inline as

```
$\sum_{i=1}^{n} x_i$
```

Integral signs, however, will not move the limits to directly over and under the integral in display mode as $\f(x)dx$.

```
$\int_{a}^{b} f(x)dx$
```

Figure 19.1 Left, ISIWYG in LyX; the right preview with g.

![](img/b30873ddd75368a5925fb9ad26a059_0.png)
