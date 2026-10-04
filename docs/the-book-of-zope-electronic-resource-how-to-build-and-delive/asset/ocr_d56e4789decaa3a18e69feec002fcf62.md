```
<tr width="100%" color="#88DD88">
<td dtml-var name="title">/</td>
<td dtml-var name="id">/</td>
<td dtml-var name="publisher">/</td>
<td dtml-var name="year_of_publication">/</td>
<td dtml-var name="genre">/</td>
<td dtml-var name="price">/</td>
<td dtml-var name="delivery_time">/</td>
<td dtml-var name="bobobase_modification_time" fmt="%d/%m/%Y - %H:%M:%S">/</td>
<td><FORM ACTION="dtml-var
name="sequence-item" url="EditForm_html">
<input type="submit" value="Edit Book">
</FORM>
<form action="DeleteConfirm_html">
<input type="hidden" name="id"
value="dtml-var name="id">
<input type="submit" value="Delete Book">
</FORM>
</td>
</tr>
<table>
<form action="CreateForm_html">
<input type="submit" value="Create a New Book">
</form>
<td dtml-var standard_html footer></td>
```

This method creates a page on which all Book instances in the folder are arranged in a table sorted by title. Each row of the table contains the property values of a Book instance and two buttons: Edit Book and Delete Book. The Create New Book button at the bottom of the table to add new Book instances to the folder.

The resulting DML method admin_html displays a screen like the one shown in Figure 10-6.

| Title | Book Id | Author | Publisher | Year of Publication | Genre | Price | Delivery Time | Last Modified | |
|---|---|---|---|---|---|---|---|---||
| A Min Full | B16630 | Tom Wolfe | Jonathan Cape | 1998 | Mystery | 19.99 | 5 days | 26/06/2001-20:56 | Edit Book Delete Book |
| The Sickness Under | B09362 | Soren Kirkegaard | PENGun USA | 1989 | Philosophy | 13.95 | 3 days | 26/06/2001-21:01 | Edit Book Delete Book |
| Create a New Book | | | | | | | | |

Figure 10-6: Administration page admin_html after you create two books