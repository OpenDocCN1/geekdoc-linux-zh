
![](img/81f56bf497dbf7f7582072400d12cb42_77_0.png)

Figure 3.13 The XSane home page

I hope that this brief overview of some of the graphics applications available under Linux has piqued your interest and if you have a need for software to work with graphics, you will try these applications. Again, an enormous amount of Free and Open Source software is out there. It's always worth checking to see whether you can find the application you're looking for among the available Free and Open Source software. I think that you will be very pleased with the quality of the available software.

# Marking Up Tables and Figures

Tables and illustrative figures are very important to technical documentation. The reason I've separated tables and figures from the rest of the graphic elements is because they can be created with DocBook markup instead of a separate program. DocBook is good, but it can't produce an 8x10 colored picture, with circles and arrows on the back of each one. It, however, creates tables and some figures, using a little help from TeX/LaTeX or MathML in the case of XML. DocBook.

# Making Tables

If you've created tables in HTML, you know that they can become complicated when you're making a table that's more than one or two rows. Unfortunately, DocBook markup is slightly more complicated than the HTML markup to create tables, and there are more options. Don't worry, I'll show them all and try to make it as simple as possible.

I should mention, you can cheat when including a table or figure. Just because you can create a table or figure with DocBook markup doesn't mean that you have to. If your output formats are limited to print output and Web output, you can get away with including the table or figure as a graphic. However, the advantage of making tables with DocBook markup is that you will be able to output to other formats that can't handle included graphics, such as plain-text format.

![](img/81f56bf497dbf7f7582072400d12cb42_78_0.png)

# Table Markup

DocBook markup has a couple of elements to create tables. There are the aptly named Table element and the popular InformalTable element. The Table and InformalTable elements are virtually the same, except that the Table element has a title, and the InformalTable does not. No title, therefore informal—get it? Actually, other than listing a list with a table in the text, there is a good reason for making a distinction between formal and informal tables. If tables include a title, then an index or listing of all tables can be automatically generated when rendering DocBook output. Nifty, isn't it?

You can create a table-like structure using the SimpleList element because it allows you to specify vertical or horizontal columns. However, this is a kludge and should not be used in place of a true table, if that's what you need. Remember, the idea behind DocBook markup is not to concern you with the look of the document but with the structure. If, indeed, you have a simple list, use that element. If your information is really a table, use that instead. The SimpleList element is covered in more detail in Appendix B, "DocBook Element Reference."

![](img/81f56bf497dbf7f7582072400d12cb42_78_1.png)

Now you will look at a small table to see how to create a table in your document.

```
<table>
<title>Example Table</title>
<tgroup cols="2">
  <thead>
  <row>
    <entry>Column 1</entry>
    <entry>Column 2</entry>
  </row>
  </thead>
  <tbody>
  <row>
    <entry>This is a cell in the table</entry>
    <entry>So is this!</entry>
  </row>
  <row>
    <entry>Column 1 Row 2</entry>
    <entry>Column 2 Row 2: This is easy!</entry>
  </row>
  </tbody>
</tgroup>
</<table>
```

As you can see, the markup to create a table in DocBook, shown in Figure 3.14, is more complicated than the markup in HTML, shown in Figure 3.15. However, it's all easy to remember after you've made a few tables.

The Table or InformalTable element begins a table. The tgroup element holds the actual content elements of the Table or InformalTable element. The tgroup and Table and InformalTable elements are not optional.

The head, tbody, and tfoot elements indicate a heading, body, or footer section of the table, respectively. The head and tfoot elements are not required in a table, but the tbody element is.

The row element holds the rows in a table, whereas the entry element actually holds the information content in the rows.

# Marking Up Tables and Figures

```
<article>
<section>
<table>
<title>Example Table</title>
<group>
<thead>
<row>
<entry>Column 1</entry>
<entry>Column 2</entry>
</row>
</thead>
<tbody>
<row>
<entry>This is a cell in the table</entry>
<entry>So is this!</entry>
</row>
<row>
<entry>Column 1 Row 2</entry>
<entry>Column 2 Row 2: This is easy!</entry>
</row>
<row>
<entry>Column 1 Row 3</entry>
</row>
</tbody>
</group>
<tfoot>
<row>
<td colspan="2">Total: 401</td>
</row>
</tfoot>
</table>
</section>
</article>
```

Figure 3.14 Example table markup

![](img/81f56bf497dbf7f7582072400d12cb42_80_0.png)

Table of Contents

Table 1. Example Table

| Column 1 | Column 2 |
|---|---|
| This is a cell in the table So is this! |  |
| Column 1 Row 2 | Column 2 Row 2: This is easy! |

Figure 3.15 Output from the markup in Figure 3.15 rendered in HTML

You might have noticed that some of the elements are not consistent with the table. Specifically, the names of the elements are not consistent.

It is possible to include a subtable within the table by using markup.

```
<!DOCTYPE article PUBLIC "//OASIS//DTD DocBook V3.0//EN">
<article>
<title>Example Table</title>
<tgroup cols="2">
<thead>
<row>
<entry>Column 1</entry>
<entry>Column 2</entry>
</row>
</thead>
<tbody>
<row>
<entry>This is a cell in the table</entry>
<entry>So is this!</entry>
</row>
</tbody>
</tgroup>
</article>
```

The advantage of making tables with DocBook markup is that you will be able to output to other formats that can't handle included graphics, such as plain-text format.

If your output formats are limited to print output and Web output, you can get away with including the table or figure as a graphic.

For more information on the CALS Table, you can check the documentation found at this URL:
http://www.oasis-open.org/html/a502.htm

![](img/81f56bf497dbf7f7582072400d12cb42_82_0.png)

# Making and Including Figures and Equations

There are a few ways you can go about including figures and equations in DocBook. I've already talked about including standard images created in programs like Adobe Photoshop and GIMP. In the next section you will look at making figures and equations with markup.

# Using LaTeX for Figures and Equations

Because LaTeX is a complicated markup language, I'm going to cheat here. Rather than try to give you a full tutorial on LaTeX, which is well beyond the scope of this book, I'll share a nifty Open Source tool with you that can use to generate LaTeX.

LyX is a program that allows you to create LaTeX markup, DVI output, and even PostScript output. Even better, LyX has great features for working with mathematical equations.

![](img/81f56bf497dbf7f7582072400d12cb42_82_1.png)

As you can see in Figure 3.16, LyX comes loaded for create equations. How do you use these wonderful tools with DocBook? One way is to use LyX to create a PostScript file for inclusion with your document. However, as mentioned before, you must have an Encapsulated PostScript file to include as an image, not a plain PostScript file. If you generate a PostScript file, you must use something like The GIMP or Adobe Photoshop to convert the PostScript file to EPS. This might seem like a lot of steps, but does guarantee that your equation will look exactly as you want to.

> DVI, or Device Independent, is a printable file created from LaTeX or TeX. DVI is produced as an intermediate format by Jade or OpenJade to create PostScript or other files.
