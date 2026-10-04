
## 9.3.9 Creating Help Topics

You can create help topics for each view that will be available for the various views you specify for the ZClass. Suppose you want to be able to access help text by clicking a Help button as soon as you click a book—something like the setup in Figure 9-21.

![](img/43a28cce5475b2f487bf455365567fb6_193_0.png)

To create the following help topics, open the path Product at Control_Panel, Products/Sales and click Help (Sales).

- 1. From the menu, select Add Help Topic.
- 2. In the Id field, enter the word Content, and in the Title field, enter Contents of a Book Object.
- 3. Click-Add. (See Figure 9-22.) Edit this object's contents by clicking Contents (Contents of a Book Object). You can now enter some help text to be displayed when you click the Help button, as in Figure 9-23.

![](img/43a28cce5475b2f487bf455365567fb6_193_1.png)

## Help Topic at: /Control_Panel/Products/Sales/Help/Content

You may edit the source for this document using the form below. You may also upload the source for this document as a local file. Click the Browse button to upload a file.

### Contents of a Book Object

```
<dmi-var standard_html_header>
<h2><dmi-var title></h2>
<p>Press here to list all subjects of the current book object.</p>
<dmi-var standard_html_footer>
```

![](img/43a28cce5475b2f487bf455365567fb6_194_0.png)

Figure 9-23: Editing the Contents help topic

### 9.3.9.1: Assigning the Help Topic to a View

But wait: We still need to assign the Contents help topic to the Contents view that displays the contents of a book, as shown in Figure 9-24. To do so, return to the Views tab of the BookClass ZClass; select the Content help topic from the pull-down menu in the Help Topic column for the Contents view, then click Change.

![](img/43a28cce5475b2f487bf455365567fb6_194_1.png)

Figure 9-24: Assigning a help topic to a view

Now, with Contents properly assigned, when you create a book object called "Book" in the Books folder and then click it, the Contents view is called up, and a Help button appears in the Help Topic column for the Contents view when you click it (see Figure 9-25).

### 9.3.9.2 Changing the Sequence of Views

To change the sequence of the views, currently Contents/Properties, select the checkbox of the view you want first and then click First. This sequence indicates how the buttons are arranged on the tab bar that appears when you click an object in the class.

The sequence in Figure 9-25 shows the management screen that appears when you click a Book class instance.

![](img/43a28cce5475b2f487bf455365567fb6_195_0.png)

Figure 9-25: Management screen with the available views for Book

This management screen displays the contents of the Book object (using the function manage_main, which you already assigned to the Contents view). The Book object contains no other objects.

> NOTE: Do not confuse the contents of an object with its properties; the object owns the properties, and the properties themselves are not the object. (See for yourself by clicking the Properties tab.)

## 9.3.10 Editing Properties

Use the Properties tab to edit the values of properties for a book object instance. Changes you make to properties in one instance will not affect other instances of the class. This allows each Book object derived from our BookClass ZClass to have individual property value assignments.

## Summary

Let's briefly summarize what we have accomplished. We have

- Created a simple Zone product.
- Created a ZClass in this product.
- Established properties for the ZClass.
- Created views for the ZClass.

In Chapter 10, you will learn how to use your ZClass and how to enhance your product with useful functions.

## 10 WORKING WITH THE ZCLASS

![](img/43a28cce5475b2f487bf455365567fb6_196_0.png)

This chapter continues the overview of the Zope classes (ZClasses) begun in Chapter 9 and continues the development of our product, Sales, to demonstrate the key ways in which you can use ZClasses in an application.

### 10.1 Modifying the Constructor Methods

In Chapter 9, you created basic ZClass. In this chapter, you will modify the constructor methods created by Zope (discussed in section 9.3), because the default versions contain only the bare minimum of code to create instances of our ZClass.

### 10.1 Modifying DT Methods

The four objects created by Zope when you created your ZClass include DT methods (BookClass_add), known as constructor methods. Zope uses these methods to create an instance of our ZClass in which we can code the actions needed to properly initialize our objects.

The default constructor form (BookClass_add) only contains an input box for the id of a new instance. The default constructor (BookClass_add) simply creates a Book object in the current folder (or folder) and sets that object's id to the value supplied in the constructor form. The other properties, which you created in section 9.3.7, are left to their default values. We need to modify these methods so that the other properties can be specified when an instance is created. Let’s start by modifying the constructor form, BookClass_add. At present, it looks like Listing 10-1.

### Listing 10-1: The DT method BookClass_add for Zope created the ZClass

```html
<HTML>
<HEAD><TITLE>Add Book</TITLE></HEAD>
<body BGCOLOR="#FFFFFF" LINK="#000099" VLINK="#555555">
<h2>Add</h2>
<form action="BookClass_add"><table>
<tr><th>id</th></tr>
<tr><td><input type="text" name="id"></td></tr>
<tr><td></td></tr>
<tr><td><input type="submit" value="Add"></td></tr>
</table>
</form>
</body>
</html>
```

Currently, this method displays the form shown in Figure 10-1.

![](img/43a28cce5475b2f487bf455365567fb6_197_0.png)

Figure 10-1: This input form appears after calling the default method BookClass_add

The screen shown in Figure 10-1 is used to enter the property values for a new instance. We need to add input fields for the other properties we created in our ZClass (see section 9.3.7 for information on the properties), so’s change BookClass_add as shown in Listing 10-2.

### Listing 10-2: The modified method BookClass_add used as an input for creating a new instance

```html
<HTML>
<HEAD><TITLE>Create Book</TITLE></HEAD>
<BODY BGCOLOR="#FFFFFF" LINK="#000099" VLINK="#555555">
<h2>Create Book</h2>
<form action="BookClass_add"><table>
<tr><th>Book Id</th></tr>
<tr><td><input type="text" name="id" size="60"></td></tr>
<tr><th>Title</th></tr>
<tr><td><input type="text" name="title" size="60"></td></tr>
<tr><th>Author</th></tr>
<tr><td><input type="text" name="author" size="60"></td></tr>
<tr><th>Published</th></tr>
<tr><td><input type="text" name="publisher" size="60"></td></tr>
<tr><th>Year of Publication</th></tr>
<tr><td><input type="text" name="year_of_publication" size="60"></td></tr>
<tr><th>Genre</th></tr>
<td><select name="genre">
<dtml-in name="book_genre sequence-item">
<option value="dtml-var sequence-item">
<dtml-var sequence-item></option>
</dtml-in>
</select></td></tr>
<tr><th>Price</th></tr>
<tr><td><input type="text" name="price" size="60"></td></tr>
<tr><th>Delivery Time</th></tr>
<tr><td><input type="text" name="delivery_time" size="60"></td></tr>
<tr><td></td><td><input type="submit" value="Create"></td></tr>
</table>
</form>
</body>
</html>
```

When creating your constructor form, make sure that the name and capitalization of each input box matches exactly its property in the ZClass.

Figure 10-2 shows our new constructor form:

| Create Book | |
|---|---|
| Book Id | |
| Title | |
| Author | |
| Publisher | |
| Date of Publication | |
| Genre | Romantic Novel |
| Price | |
| Delivery Time | |
