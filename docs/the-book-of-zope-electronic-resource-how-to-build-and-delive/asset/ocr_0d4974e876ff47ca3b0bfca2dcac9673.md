# Take ownership

From Zope 2.2.0 onward, this permission adds a button labeled "Take ownership" to the Ownership screen, provided the current user does not already own the object. Although the role Manager is normally given all permissions by default, this right is not. This permission is assigned by default only to the Owner role.

# Undo changes

This very important permission makes the Undo tab appear in the management screen. To use the Undo changes permission, you may need to set additional permissions on what you want to undo. In general, though, if you can perform an action, you can also undo it.

> As of Zope 2.2.0, the Undo screen displays only actions carried out in the current folder or its subfolders, not all actions in the Zope installation as was previously the case.

# View

When this permission is set for an object for a given role, users assigned that role can view the object in the third tier view. This permission is often set in conjunction with Access contents information (above). It does not allow users to access the management screen using the /manage URL extension.

> This permission is granted by default to the Anonymous role.

# View history

Users with this permission see a History tab in DTML documents and methods. This tab leads to the History view, which lists all actions carried out on the current object, from which you can compare the current version of a DTML document with a previous version.

# View management screens

Users with this permission can access the management screen using the URL for an object together with the /manage URL extension. For example, the URL to access the management screen for a DTML document named index_html in a folder named My_Folder would be http://localhost:8080/My_Folder/index.html.

This permission does not allow a user to do more than view these screens. Additional permissions must be granted for a user to be able to add, edit, or delete objects, for instance.

# 7.3.2 Permissions for Folderish Objects

As mentioned in Section 7.3, folderish objects have many more available permissions than non-folderish ones. These include the permissions for nonfolderish objects, permissions created as a result of new product installations, and permissions provided by Zope for folders. We will now take a look at this last group of permissions: permissions provided by Zope for folders.