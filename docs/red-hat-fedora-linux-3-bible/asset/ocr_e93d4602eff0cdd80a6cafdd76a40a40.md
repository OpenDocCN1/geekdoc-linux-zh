```
.sp
.EQ
a sup 2 + - b sup 2-lineup = - 1000
.EN
.sp
.EQ
x sup 3 + - y sup 3 + - z sup 3-lineup = - 1400
.EN
```

If this appeared in a memo called memoeqn.mm, the memo would be preprocessed by eqn and then sent to the printer using the following command:

```
$ groff -tpr -l -mm -e memoeqn.mm
```

All data between the .EQ and .EN macros are interpreted as equations. The resulting output from the equation would appear as shown in Figure 6-7.

![](bbox=[0.12, 0.39, 0.38, 0.46])

Figure 6-7: Produce equations in documents with the use of the eqn command's .EQ and .EN macros.

To create a table in a Groff document, use the .TS and .TE macros of the tbl preprocessor. The following is an example of the markup used to produce a simple table.

```
.TS
center, box, tab(;;);
c n s
c c | c
l | l | l.
Mergers and Acquisitions Team
=
Employee:Title:Location
=_
Jones, James:Marketing Manager:New York Office
Smith, Charles:Sales Manager:Los Angeles Office
Taylor, Sarah:R&D Manager:New York Office
Walters, Mark:Information Systems Manager:Salt Lake City Office
Zuer, Mike:Distribution Manager:Portland Office
.TE
```

After the .TS macro starts the table, the next line indicates that the table should be centered on the page (*center*) and surrounded by a line box and that a colon will be used to separate the data into cells (*tab(;;)*). The next line shows that the heading should be centered in the box (*c*) and should span across the next two cells (*s s*). The line after that indicates that the