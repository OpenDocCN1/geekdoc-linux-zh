```
```
1   |  1   |  1.
Mergers and Acquisitions Team
-
Employee::Title::Location

Jones, James::Marketing Manager::New York Office
Smith, Charles::Sales Manager::Los Angeles Office
Taylor, Sarah::R&D Manager::New York Office
Walters, Mark::Information Systems Manager::Salt Lake City Office
Zur, Mike::Distribution Manager::Portland Office

.TE
```
```

After the .TS macro starts the table, the next line indicates that the table should be centered on the page (center) and surrounded by a line box and that a colon will be used to separate the data into cells [tab(:)]. The next line shows that the heading should be centered in the box (c) and should span across the next two cells (s s). The line after that indicates that the heading of each cell should be centered (c c c) and that the data cells that follow should be left justified (1 1 1).

> **CAUTION:** There must be a period at the end of the table definition line. In this case, it is after the 1 | 1 | 1. line. If the period is not there, tbl will try to interpret the text as part of the table definition. In this case, tbl will fail and stop processing the table, so the table will not print.

The rest of the information in the table is the data. Note that the tab separators are colon characters (:). When the table is done, you end it with a .TE macro. If the table were in a memo called memotbl.mm, tbl could preprocess the memo and then send it to the printer using the following command:

```
```bash
$ groff -Tps -1 -mm -t memotbl.mm
```
```

Data between .TS and .TE macros are interpreted as tables (see Figure 6-8).

| Employee | Title | Location |
| :--- | :---: | :--- |
| Jones, James<br>Smith, Charles<br>Taylor, Sarah<br>Walters, Mark<br>Zur, Mike | Marketing Manager<br><br>Sales Manager<br><br>R&D Manager<br><br>Information Systems Manager<br><br>Distribution Manager | Jones, James<br>Smith, Charles<br>Taylor, Sarah<br>Walters, Mark<br>Zur, Mike |


**Figure 6-8:** Set how text is justified and put in columns with the use of the tbl command’s .TS and .TE macros.

The PIC macros (.PS and .PE) enable you to create simple diagrams and flow charts to use in Groff. PIC is really qualified to create only simple boxes, circles, ellipses, lines, arcs, splines, and some text. The following is some PIC code that could be in a Groff document:

```
```
.PS
box invis  "Start" "Here"; arrow
```
```