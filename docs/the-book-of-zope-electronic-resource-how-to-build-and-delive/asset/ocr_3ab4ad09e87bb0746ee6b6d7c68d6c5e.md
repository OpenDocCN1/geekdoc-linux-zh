Using the tag you can, for example, iterate through the elements in a list
in order to display them in a table. For example, consider the following code:

```
1: <dml-in exp=['Henderson', 'Jackson', 'Johnson', 'Jones', 'King', 'Smith']>\n2: <dml-if name="sequence-start">
3: <table>
4: <tr>
5: <th>sequence-start?</th>
6: <th>sequence-end?</th></th>
7: <th>sequence-index</th>
8: <th>sequence-itemc</th>
9: </tr>
10: </dml-if>
11: <dml-if name="sequence-odd">
12: <tr bgcolor="#eeee">
13: <dml-else>
14: <tr>
15: </dml-if>
16: <td><dml-var name="sequence-start"></td>
17: <td><dml-var name="sequence-end"></td>
18: <td><dml-var name="sequence-index"></td>
19: <td><dml-var name="sequence-item"></td>
20: </tr>
21: </dml-if name="sequence-end">
22: </table>
23: </dml-if>
24: The sequence is empty.
25: </dml-in>
```

In this example, a list is passed as an expression to the starting in tag (Line
1). The tag first determines whether the list is empty (contains no items); if so,
a message to this effect is output using the list tag (Lines 24 and 25). Otherwise,
t code in the body is executed for each item in the list in turn.

When we start the list, dml sets the variable sequence-start to true. We test
for this condition using dml-if (Line 2), and a table header is defined when it
true (3 through 9). For each item in the list, a row is added to the table con-
taining values provided by some of the variables defined by the in tag.
dim-in variable sequence-order is tested to determine whether to show the row
Line 11). If this value is true, the row is showed (Line 12), otherwise it is not
Line 14). When the last item of the list is iterated, dml-in sets the variable
sequence-end to true. We test for this condition using dml-if (Line 21), and the
table is closed when it is true. The rendered output of this code would look like
Figure 4-7 viewed by a browser.