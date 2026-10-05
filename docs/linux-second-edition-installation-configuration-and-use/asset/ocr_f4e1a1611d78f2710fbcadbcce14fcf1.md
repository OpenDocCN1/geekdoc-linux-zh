# HINTS AND TRICKS 649

language in the spell check options dialog, or (as a root) you establish links from german.* to deutsch.

```
root# cd /usr/lib/ispell
root# In -s deutsch.aff german.aff
root# In -s deutschixg.aff german.hash
```

A second problem with non-English language documents is the coding of special characters: in any word containing a foreign language special character, the spell checker suspects an error. Here too, the remedy is simple: just activate the INPUT ENCODING for ISPELL in the spell check options dialog.

A very disturbing peculiarity of the spell check in the current version of LaTeX/KX is that during replacement of incorrectly spelled words the character formatting (for example, italicized emphasis) is lost.

# Inserting page breaks

LaTeX has no own command for inserting page breaks. Instead, you can force a page break before or after a paragraph in the LAYOUT PARAGRAPH dialog.

# Comments

With INSERTNOTE you can enter comments to your text which will not be printed. An alternative is paragraphs of the comment type.

# Errors

Theoretically LaTeX should always produce correct LaTeX code. In practice, however, sometimes errors may occur during translation. LaTeX errors are shown in LaTeX by a button. When you click on this button, you get some (mostly incomprehensible) information on the origin of the error. So what are we to do now The most effective solution is to delete the corresponding LaTeX element (for example a figure) and to enter it again. Furthermore, you must remove the error button from the text. Then just try the translation. LaTeX professionals may also want to use a text editor to edit the *.tex file and correct the error directly. However, extreme caution is highly recommended. In any case, do not forget to create a backup of your *.tex file!

In rare cases LaTeX may also hang (if for example the LaTeX construction – as a table – has got lost). You recognize this from the fact that the LaTeX translation just not to stop and LaTeX is blocked. In this case, you need to look for the LaTeX process in a shell with ps and terminate it with kill. (A decidedly more user-friendly solution is provided by KDE/Gnome with ktopg.)

As often in this book, this chapter can only give a first introduction. LaTeX obviously provides many more document layout possibilities, but the space is not sufficient to describe them all. Please consult the excellent online documentation!

![](bbox=[0.135, 0.796, 0.195, 0.866])