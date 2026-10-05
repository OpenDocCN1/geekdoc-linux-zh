# Tables

Producing clearly structured tables in LaTeX is easier thanks to WYSIWYG features, but handling is still far from being intuitive. (Here, the symbol bar gives KLX a clear advantage over LyX.) Furthermore, in comparison with true text processing programs, the layout possibilities are severely restricted. however, this is not the fault of LyX, but rather LaTeX.

Tables belong to the very few features that may cause stability problems in both LyX and KLX. The only crash that occurred during writing of the German version of this chapter concerned a table operation. (However, even in that situation, KLX still succeeded in carrying out a complete emergency backup – wouldn't it be nice to see Word do the same?)

When you insert a new table into your document by means of INSERT TABLE, it will look like this (initially, quite obviously, without contents).

| Title 1 | T2 | T3 | T4 | T5 |
|---|---|---|---|---||
| Line 1 | A | B | C | D |
| Line 2 | EE | FF | GG | HH |
| Line 3 | III | JJJ | KKK | LLL |

LyX treats the table as a whole as if it were a paragraph. Thus, if you wish to range the whole table left or right, you need to use LAYOUT PARAGRAPH.(Before after a table, LyX inserts a vertical space of 3 mm. This too can be changed or deleted in the PARAGRAPH dialog)

It is useful to put tables into a float environment by means of INSERT FLOAT. This makes the table's position on the page variable, and can avoid big holes when laying out the pages. (Labeling of tables in float environments works in the same way as with figures – see above.)

![](bbox=[0.26, 0.663, 0.755, 0.856])

Figure 19.6 On top, the KLX table symbol bar: below, the corresponding LyX dialog.