
# 646 LYX - LATEX MADE EASY

![](img/b30873dd3d753687a59253fb9ad26a0b_673_0.png)

## 19.4 Maths

Input of maths is started via the commands of the MATH menu. By default, maths entries are integrated into the flowing text (such as the following $x^2$). With MATH/DISPLAY, however, a formula can also be highlighted and thus appears as a separated paragraph:

$$\int \frac{\sqrt{3}}{n} ds$$

The elements of a formula (fractions, exponent and index, integral and sum, and so on) are assembled by means of MATH menu commands. Input of special maths symbols can be carried out either via mouse click or via the keyboard. The first variation is more intuitive: with MATH/PANEL you open a small dialog which contains a lot of submenus for the majority of the special characters defined in $\LaTeX$. Those who have already gained some experience with LyX will probably prefer keyboard input of math symbols (more about this on page 656).

![](img/b30873dd3d753687a59253fb9ad26a0b_673_1.png)

## MATHS 647

LyX has neither a MATH menu nor a dialog as the one mentioned above. Their functions are instead integrated into a single symbol bar. An essential advantage over LyX consists in the fact that the input focus always remains inside the document.

LaTeX as in LyX, the limits of an integral or sum variable are indicated as exponents or indices. Just place the insertion point after the corresponding symbol (f, ∑, ∫, and so on), then enter the values with MATH|EXPONENT (or ') or with MATH|INDEX (or _).

### Brackets

LaTeX automatically adjusts the size of brackets to the contents of the enclosed elements (for example, a matrix). However, this works only if the brackets are entered either via the corresponding MATH panel dialog or via the keyboard shortcuts Alt+[ or Alt+M[. Direct input of bracket characters from the keyboard does not lead to the desired result.

### Formula numbering

The easiest way to free-standing formulas is to assign a label (INSERT|LABEL). In LyX, this label is now displayed over the formula: in the page preview the label is replaced with a right-angled number.

$E=mc^2 (19.1)$

### Spacing

LaTeX does not feature input of spaces in formulas – it takes care of spacing itself. A Spacebar in LyX therefore does not insert a space character, but leaves the currently active formula level. If you wish to insert a small space between two symbols (for example, to make clear that in multiplication ab is the product of two variables and not the variable ab), you simply use Ctrl+Spacebar. For adjustments of the layout, additional spacing elements are available (even a negative one, to put two elements closer to each other). In LyX, they can be entered via the SPAC panel.

### Function names

To ensure that the names of mathematical standard functions are set upright and not in italics, like variables), they must be simply entered via the keyboard. Instead, you select them from the function list of the MATH panel or use the corresponding LaTeX code (for example $\$\sin$ for the sin function).

### Matrices

Empty matrices can be inserted via the appropriate button of the MATH panel or the symbol bar. Think about the size the matrix should have – it cannot be changed at a later stage! Matrices are not automatically enclosed in brackets. You can enter the pair of brackets with Alt+[M[ before you create the matrix, or select all elements of an existing matrix and then execute the bracket command of the MATH panel or the symbol bar.

```
$$\begin{matrix} a & 1+b & \sqrt{c} \\ a^2 & 2+b^2 & c \\ a^3 & 3+b^3 & \sqrt{3} \end{matrix}$$
```

## 19.5 Hints and tricks

**n-dashes**

In LyX, en-dashes are entered as two consecutive minus signs, that is, --.

**Word spacing**

To extend the individual lines of a paragraph to the same length in justified typesetting, $TeX$ inserts an equal amount of space between all words (of the same line). After a full stop (end of sentence), this space is a bit wider. If example, for an abbreviation, a normal space is used after a full stop, a symbol may be inserted between the full stop and the space in $TeX$ mode (input via $\text{Alt}+\text{Ctrl}+\text{C}$, $\text{V}$, $\text{Alt}+\text{T}$). In LyX this looks like: Dr.V Weber. To prevent two words from being separated by a linebreak, a fine space can be specified by $\text{Ctrl}+\text{Space}$, for example 3 cm.

**Hyphenation**

$TeX$ does not always recognize all possible hyphenations (or even hyphenates correctly). In such cases, you can use $\text{Ctrl}+-$ to insert a soft hyphen which $TeX$ will use if needed.

**Quotation marks**

Similarly to Emacs in $TeX$ mode, LyX tries to use typographic quotation marks of the “citation” form. (Although both quotation marks have been input with “”, they have a different shape and constitute a group). If you need a normal (‘’ quotes–for example when entering commands, program listings, and so on–you need to use $\text{Ctrl}+-$

**Spell check**

LyX has no spell check of its own, but resorts to the well-established $spell$ program of the Unix/Linux world. This program is installed together with the word tables for the desired language, you can start the spell check with $\text{EDIT}\text{SPELLCHECKER}$, or still, with $\text{F7}$. (The spell check starts at the current cursor position).

In Non-English language documents (setting in $\text{LAYOUT}\text{DOCUMENT}$, $spell$ usually does not find the dictionary. The reason: LyX for example, ‘german’ as the required language, the name of the dictionary, however, is ‘deutsch’. The problem can easily be solved: either you explicitly specify ‘deutsch’ as the required language in the spell check options dialog, or (as a root) you establish links from german.* to deutsch.

```
root# cd /usr/lib/ispell
root# In -s deutsch.aff german.aff
root# In -s deutschixg.aff german.hash
```

A second problem with non-English language documents is the coding of special characters: in any word containing a foreign language special character, the spell checker suspects an error. Here too, the remedy is simple: just activate the INPUT ENCODING for ISPELL in the spell check options dialog.

A very disturbing peculiarity of the spell check in the current version of LaTeX/KX is that during replacement of incorrectly spelled words the character formatting (for example, italicized emphasis) is lost.

**Inserting page breaks**

LaTeX has no own command for inserting page breaks. Instead, you can force a page break before or after a paragraph in the LAYOUT PARAGRAPH dialog.

**Comments**

With INSERTNOTE you can enter comments to your text which will not be printed. An alternative is paragraphs of the comment type.

**Errors**

Theoretically LaTeX should always produce correct LaTeX code. In practice, however, sometimes errors may occur during translation. LaTeX errors are shown in LaTeX by a button. When you click on this button, you get some (mostly incomprehensible) information on the origin of the error. So what are we to do now? The most effective solution is to delete the corresponding LaTeX element (for example a figure) and to enter it again. Furthermore, you must remove the error button from the text. Then just try the translation. LaTeX professionals may also want to use a text editor to edit the *.tex file and correct the error directly. However, extreme caution is highly recommended. In any case, do not forget to create a backup of your *.tex file!

In rare cases LaTeX may also hang (if for example the LaTeX construction – as a table – has got lost). You recognize this from the fact that the LaTeX translation just not to stop and LaTeX is blocked. In this case, you need to look for the LaTeX process in a shell with ps and terminate it with kill. (A decidedly more user-friendly solution is provided by KDE/Gnome with ktopg.)

As often in this book, this chapter can only give a first introduction. LaTeX obviously provides many more document layout possibilities, but the space is not sufficient to describe them all. Please consult the excellent online documentation!

![](img/b30873dd3d753687a59253fb9ad26a0b_676_0.png)
