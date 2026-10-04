If you do not display the result of the method on the current page, use the call tag instead of the var tag:

```
<html-call expr="object.method()">
```

object above represents the Zope object (DTML document, User Folder, and so on) with whom you wish to do something. If you omit object, Zope assumes you wish to execute the method on the object at the top of the name-space stack.

The modules Role.py and User.py are in the system under /lib/python/AccessControl. Let's begin with the Role.py module.

# Methods for the Module Role.py

The following methods, in file Role.py in the Zope directory lib/python/Access-Control, are active on any Zope object with a Security tab, which is nearly all Zope objects.

acquiredRolesUsedBy(permission)

The result of this method is 'CHECKED' (for use in an HTML checkbox), if the Acquisition permission settings are active for the object's permission named permission. If not, an empty string is returned.

has_local_roles()

This method returns the number of local roles set for the object.

get_local_roles()

This method produces a list of tuples (a special immutable list), each of which contains the username as the first element and a list of local roles set for them as the second element.

For example:

```
[['TestUser1', ['Manager']],
['TestUser2', ['Owner']],
['manager', ['Owner']]
```

get_valid_userids()

This method gives a combined list of all user names from all User Folders the object's acquisition chain.

get_local_roles_for_userid(userid)

This method results in a list of all set local roles for the specified user name in userid.