# Add ZCatalogs

When the permission Add ZCatalogs is set, you can create a ZCatalog in a folder. ZCatalogs are folder objects that allow you to index and query other Zope objects. To find and index objects in the ZCatalog, you must have the permission Manage ZCatalog Entries.

The permission Search ZCatalog allows a user search the ZCatalog for objects, but no other operations, such as management, can be performed.

# Add Zope Tutorials

Zope versions since 2.2.0 include an introductory Zope tutorial. To view it, you must first create a Zope Tutorial object, which you'll only be able to do if you have this permission.

# Change Database Methods

This permission must be assigned for you to be able to change SQL methods. You must also set this permission in order to display the Test tab in the management screen and to set an SQL method.

# Change External Methods

This permission allows you to modify External Method objects and to reload the external file corresponding with the External Method, if it has been modified.

# Change Images and Files

> NOTE

When you upload a new version of an image or file, the old version may still be displayed if it is still in your computer's cache. To remedy this, empty your browser cache.

# Change Python Scripts

This permission allows you to save changes made to Python Scripts (available in Zope 2.3 and later).

# Change Versions

With this permission, you can open an existing version in the Properties screen and change its title. To view the other screens for an object, you will need the permissions Join/leave Versions and Save/ discard changes.

> NOTE

You may be asked to enter your password when you confirm the title change, because the OK button in the message "Your changes have been saved" refers to the version's join/leave screen in the background, for which you may not have permissions. Although Zope responds as you need the permission join/leave Versions, your changes to the title will still be saved.

# Change cache managers

This permission is needed to change the objects cached by a RAM Cache manager object.