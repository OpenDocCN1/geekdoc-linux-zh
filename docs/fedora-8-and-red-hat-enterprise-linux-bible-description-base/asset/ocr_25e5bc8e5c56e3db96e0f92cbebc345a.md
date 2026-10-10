```
box "Step 1"; arrow
circle "Step 2"; arrow
ellipse "Step 3"; arrow
box "Step 4"; arrow
box invis = "End"
,PE
```

After the .PS, the first line indicates an invisible box (invis) that contains the words Start Here, followed by an arrow. That arrow connects to the next box containing the words Step 1. The next elements (connected by arrows) are a circle (Step 2), an ellipse (Step 3), another box (Step 4), and another invisible box (End). The .PE indicates the end of the pic drawing.

If these lines appeared in a document called memopic.mn, you could preprocess the PIC code and print the file using the following command:

```
$ groff -Tps -1 -mm -p memopic.mn
```

Figure 6-9 shows an example of this drawing.

![](bbox=[0.18, 0.4, 0.88, 0.52])

# Text processing with TeX/LaTeX

TeX (pronounced tech) is a collection of commands used primarily to produce scientific and mathematical typeset documents. The most common way to use TeX is by calling a macro package. The most popular macro package for TeX is LaTeX, which takes a higher-level approach to formatting TeX documents. TeX and LaTeX tools are contained in the texex-latex package.

> NOTE: The texex\* packages needed to use the TeX examples shown in this chapter are found on the DVD that accompanies this book.

TeX interprets the LaTeX macros from the latex format file (latex.fmt). By default, the latex.fmt and plain.fmt format files are the only ones that are built automatically when the TeX package is installed. Other macro files that you can use with TeX include:

+   - amstex — Mathematical publications, including the American Mathematical Society use this as their official typesetting system.
+   - eplain — Includes macros for indexing and table of contents.