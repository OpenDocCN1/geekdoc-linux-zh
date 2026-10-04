# 10.3.1 Working in the Books Folder with the Management Screen

Open the management screen (as shown in Figure 10-4), then add, delete, or edit a book as follows:

+   1. **Add:** Create a new book instance by selecting Book from the menu.
   Pressing Add calls the method BookClass_addForm.

+   2. **Delete:** Delete a book by activating a checkbox to the left of the object and clicking Delete.

+   3. **Edit:** Edit a book to access the following views: Contents and Properties.

Try experimenting little here by creating additional books, editing a book's properties (using the Properties view), and deleting some books. You can see that the books behave much like like the built-in Zope objects (for example, DTML documents or files).

# 10.3.2 Working with an Administration Interface

10-6 shows an administration interface for managing book objects, which you can use to create new book objects, edit book data, and delete books. You can also create a page to sell the book objects you create using a DTML method.

# 10.3.2.1 Creating admin_html

To create admin_html in the Books folder, follow these steps:

+   1. Select DTML Method from the pull-down menu.

+   2. In the id field, enter admin_html and click Add and Edit.

+   3. A field opens that contains the minimum code necessary for the method. Delete this code and enter the DTML code for the method admin_html as shown in Listing 10-4.

Table 10-4: The DTML method admin_html

```
1: <dtml-var standard html_header>
2: <table border=0 cellpadding=4 width="80%">
3: <tr width="100%" bgcolor="#44BBBC">
4: <th>Title</th>
5: <th>Book Id</th>
6: <th>Author</th>
7: <th>Publisher</th>
8: <th>Year of Publication</th>
9: <th>Genre</th>
10: <th>Price</th>
11: <th>Delivery Time</th>
12: <th>LastModified</th>
13: </tr>
14: <dtml-in expr="objectValues(['Book'])" sort=title
```

(continued on next page)