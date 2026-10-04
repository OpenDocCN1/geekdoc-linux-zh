+   • If the file is found, addDocFolder attempts to create a DTML method using the file's data and the id and title specified in the directory by calling the built-in Zone constructor method for DTML objects: manage_addDTMLMethod. If an error occurs during this process (say, if the id is illegal), then the corresponding error message is displayed.

# 15.4.2.3 Class Definitions

A class is a template to create objects (instances). We use classes to define all of an instances' attributes, which may contain variable data (such as strings, lists, and dictionaries) or other objects (such as DTMLFile objects) or may define methods that act on the instance and its data.

The main elements of the Website class are as follows (these will differ from other products):

+   • A definition of the class as a folder object, specifying Folder as the base class.
• A definition of the properties for all instances of the product (accessed via the Properties tab in the management screen) that allow the webmaster to make certain changes to the instance. (In our case, only the title property is common to all instances.)
• A definition of new tabs to appear in the management screen tab bar of each instance of the product. These new tabs can be added to existing tabs or may appear on their own.
• The assignment of permissions to associated with specific instance methods of the product in Zope (accessed via the Securities tab in the management screen). These expand the security model of the instance relative to other objects in Zope.
• The definition of methods available to authenticated users logged in to an instance of the product, including methods for creating, editing, and deleting users.

We'll call the Website class "Website." In a Python class definition, you can specify base classes (separated by commas) in parentheses following the class name. All attributes defined in the base classes become attributes of the new class you are defining (called a subclass). The class acts as an extended Zope folder, and for can therefore use the built-in Zope Folder class as a base class for Website. By using Folder as a base class, we get all of the capabilities of the Folder class in the Website class. As a result, instances of the Website can contain other objects, just as folders do; this is an example of inheritance.

> The Folder class has other functionality, such as a property sheet, and it contains many of the standard management screens. If you do not need all of these capabilities in your class, but you still need it to act folderish, you can use ObjectManager as a base class instead (OFS.ObjectManager.ObjectManager).