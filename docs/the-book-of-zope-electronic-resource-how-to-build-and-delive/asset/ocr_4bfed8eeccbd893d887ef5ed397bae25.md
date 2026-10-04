Thus, you could associate existing instances with the new ZClass by copying the Class ID of the original ZClass into the new one and deleting the original ZClass. You must be very careful doing this, because this can easily break all of the original ZClass's instances. You can also specify an image on your local computer and use it as an icon for the ZClass instances so that they have icons in the management screen like other objects.

![](bbox=[0.218, 0.155, 0.735, 0.385])

Figure 9-11: Changing ZClass inframatian after it has been created

# 9.3.4.3 Views Tab

Click Views to create views for your ZClass instances. A view consists of a tab in the management screen's tab bar and a method called when the tab is clicked. To understand this better, the bottom of Figure 9-12, which contains a view called Contents, automatically created by Zope. The management screen in Figure 9-11 shows an example of the Basic view, in which you can change certain information relating to the ZClass.

Views allow you to perform various functions on objects, including:

+   - Displaying and editing an object's contents
- Editing an object's properties
- Previewing an object
- Changing an object's security permission

The Contents in Figure 9-12 shows a tab called Contents, which appears in the tab bar if you click a class instance. If you open the folder Books and click the object Book01, the Contents tab appears in the tab bar. If you then click Contents, the Python method manage_all is called; this method (inherited from the ObjectManager base class) displays the contents of a folderish object.

We can create views for our BookClass that will allow us to inspect and modify the properties of an object and view it as it appears to users in the third tier.