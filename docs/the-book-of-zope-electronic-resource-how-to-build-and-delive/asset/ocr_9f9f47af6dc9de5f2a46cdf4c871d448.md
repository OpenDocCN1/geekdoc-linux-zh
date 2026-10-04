# 9.3.9.2 Changing the Sequence of Views

To change the sequence of the views, currently Contents/Properties, select the checkbox of the view you want first and then click First. This sequence indicates how the buttons are arranged on the tab bar that appears when you click an object in the class.

The sequence in Figure 9-25 shows the management screen that appears when you click a Book class instance.

![](bbox=[0.218, 0.175, 0.813, 0.269])

Figure 9-25: Management screen with the available views for Book

This management screen displays the contents of the Book object (using the function manage_main, which you already assigned to the Contents view). The Book object contains no other objects.

> > NOTEnDo not confuse the contents of an object with its properties; the object owns the properties, and the properties themselves are not the object. (See for yourself by clicking the Properties tab.)

# 9.3.10 Editing Properties

Use the Properties tab to edit the values of properties for a book object instance. Changes you make to properties in one instance will not affect other instances of the class. This allows each Book object derived from our BookClass ZClass to have individual property value assignments.

# Summary

Let's briefly summarize what we have accomplished. We have

+   * Created a simple Zone product.
* Created a ZClass in this Zone product.
* Established properties for the ZClass.
* Created views for the ZClass.

In Chapter 10, you will learn how to use your ZClass and how to enhance your Zone product with useful functions.