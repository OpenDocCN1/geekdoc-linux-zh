role can carry out actions on object defined in permission. If a user lacks this permission, a permission is neither set in the object nor via acquisition for any role assigned to the user.

For example, a user with the role Friends can open a DTML document in the third tier if the permission View has been assigned to the Friends role for that document. The user cannot view the management screen, however, if the permission View management screens is not assigned to the Friends role for that document.

# Access contents information

This permission allows a user to view information, such as the Title or id, relating to the object for which the permission is set. Take, for example, the standard content of a DTML document, as shown in Listing 7-1. Zope automatically inserts this content into the document by default when you create a new DTML document. This code also appears in the DTML document index_html, created automatically by Zope if you activated Create public interface when creating a new folder.

# Listing 7-1: Standard Content of a DTML Document

```
<dtml-var standard_html_header>
<h2><dtml-var title_or_id></h2>
<p>
This is the <dtml-var id> Document.
</p>
<dtml-var standard_html_footer>
```

<dtml-var title_or_id> returns the Title, if there is no Title, the id of the object; <dtml-var id> returns only the id of the object.
If a user lacks this permission on a DTML document with this code, they will be unable to render the document, and thus unable to view if they have the View permission. Zope requires that the user log in as a user who belongs to a role permitted to view this object information. You often need to set this permission in conjunction with View to allow users to view a DTML document.

> This permission is granted by default to the Anonymous role.

# Change DTML Documents/Change DTML Methods

These permissions must be set so that changes to existing DTML documents and methods can be saved. If a user lacking the appropriate permission attempts to save changes by clicking the Change button, the user is asked to enter a password. Without this password—that is, without the appropriate permission—the user can only view the source code of the DTML document or method in the Edit screen.