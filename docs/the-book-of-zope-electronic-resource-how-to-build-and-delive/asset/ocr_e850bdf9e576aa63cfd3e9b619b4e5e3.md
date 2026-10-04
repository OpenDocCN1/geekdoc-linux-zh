```
25: <OPTION VALUE="&lt;html-var name=sequence-item">
26: &lt;html-var name=sequence-item">
27: &lt;/OPTION>
28: &lt;/html-in>
29: &lt;/SELECT&gt;td
30: &lt;/tr>
31: <tr><th>Price</th>
32: <td>&lt;input type=text name=price size="60"&gt;</td>
33: &lt;/tr>
34: <tr><th>Delivery Time</th>
35: <td>&lt;input type=text name=delivery_time size="60"&gt;</td>
37: &lt;/tr>
38: <tr><th>&nbsp;&nbsp</th>
39: <td>&lt;input name="create" type=submit value="Create">
40: &nbsp;&nbsp;&nbsp;
41: &lt;input name="cancel" type=submit value="Cancel"&gt;</td>
42: &lt;/tr>
43: &lt;/table>
44: &lt;/form>
45: &lt;html-var_standard_html_footer>
```

CreateForm_html displays the management screen shown in Figure 10-7 and very similar to the BookClass_addForm method we adapted in Section 10.1.1.
Compare the methods in Listing 10-2 and in Listing 10-5. The screen in Figure 10-7 is used for the administration interface and uses the DTML Method admin_html.

# Create Book

| Book Id |
|---||
| Title |
| Author |
| Published by |
| Year of Publication |
| Genre | Fantasy |
| Price |
| Delivery Time |
| | Create | Cancel |

Figure 10-7: The page created by CreateForm_html