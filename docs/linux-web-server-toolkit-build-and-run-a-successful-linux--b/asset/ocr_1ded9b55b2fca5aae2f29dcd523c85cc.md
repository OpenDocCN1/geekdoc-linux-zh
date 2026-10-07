# Chapter 9: Creating HTML Pages

A table is defined by the <TABLE> tag and ends with a </TABLE> tag. Between these tags, each row starts with a <TR> tag (Table Row) and ends with a </TR> tag. The first row can optionally be a <TH> tag instead of <TR> tag. Heading. Within each <TR> pair (or <TH> pair) are the cells, each one starting with a <TD> and ending (optional but highly recommended) with a </TD> tag. That's all there is to it. Here is a listing for a table that contains cell numbers:

```
<TABLE>
<TR> <TH>h1</TH> <TH>h2</TH> </TR>
<TR> <TD>a1</TD> <TD>a2</TD> </TR>
<TR> <TD>b1</TD> <TD>b2</TD> </TR>
<TR> <TD>c1</TD> <TD>c2</TD> </TR>
<TR> <TD>d1</TD> <TD>d2</TD> </TR>
</TABLE>
```

This example might look something like Figure 9-11 in your browser. Not all the parameters are shown in the preceding text;, it's simplified so that it's easy to read.

![](bbox=[0.063, 0.43, 0.516, 0.626])

Figure 9-11: Tables can be used for many purposes. This simple example shows tabular data in a standard format. Many options are available.

The power of tables comes in their options, which I'm not going to explain in detail. Table options (mostly in the form of parameters added to the tags shown here, plus a few additional tags) allow you to:

+   - join cells together (so one visual space spans several cells of the table's structure)
- set the border style (or remove borders) from any cell individually
- include images and nested lists within a single cell
- include nested tables within a single cell