# Index

Slightly more work is required to create an index. Here, you first need to insert the required entries by means of INSERT INDEX ENTRY. The syntax is the same as in LaTeX (see page 611). The Index itself is inserted (usually at the end of the document) by means of INSERT LIST AND INDEX LIST.

# Cross references

If you wish to make use of cross references, you must first insert a text label with LABEL and give it a name. Subsequently, you can insert a page or section number (reference) by means of INSERT CROSS-REFERENCE. The LaTeX document shows only a small box at this position. Only the page preview displays the correct numbers. The following two references point to the beginning of this subsection: page 645 in 19.3.

# Bibliography, References

LaTeX can help manage a simple reference section (bibliography). The entries in this list need to be at the end of the document. For this purpose, you insert a new paragraph and select bibliography, as its type. In this paragraph, you can enter the references in the required format.

The peculiarity of the bibliography format is that a button with a running number appears to the left of the reference. When you click on this, you can extend the number with two reference indications, the KEY and the LABEL. The KEY is required to refer to the reference in the running text. The LABEL is the text that appears in the printed document. If you leave the label empty, all bibliography entries are simply numbered in the sequence in which they are quoted in the reference section.

To insert a reference to a bibliography entry into your text, execute INSERT CITATION REFERENCE and select the required entry from a selection list. (Caution: LaTeX displays the content of the KEY; the content of the LABEL is only shown in the final document!)

An example: a very compact introduction to LaTeX and in particular to LaTeX is given by [Et98]. The entry in the References section looks as follows.

+   [Et98] Etrich, Matthias: Schön schreiben mit Linus. LaTeX. In: PC Magazin 8/98, WEKL-Verlag 1998, S. 24-27.

The method of creating a bibliography described above corresponds to the LaTeX commands \cite and \bibitem (see page 608). In future versions, LaTeX will probably also support the LaTeX utility program bibtex, which provides much more advanced features for managing bibliographic references.