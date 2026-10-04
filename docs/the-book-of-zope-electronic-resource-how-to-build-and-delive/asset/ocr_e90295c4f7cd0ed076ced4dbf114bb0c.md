# 15.4.2.11 The editWebsiteUser Method

The editWebsiteUser method (shown in Listing 15-5) is very short, because we do not initially need to check whether user to be modified already in the User folder acl_users. The method editWebsiteUser() is called in the DTML method WebsiteUsers_List, which generates a list of users present in the User folder.

Listing 15-5: The method editWebsiteUser() for the Website product

```
# Allow users with the "Manage users" permission access to this method
security.declareProtected('Manage users', 'editWebsiteUser')

def editWebsiteUser(self, name, pwd, confirm, domains, roles, REQUEST, RESPONSE):
    # "Changes existing WebsiteUser"
    self.acl_users.changeUser(name,pwd,confirm,domains)
    return MessageDialog(
        title='User changed',
        message='The user has been changed.',
        action='index.html'
    )
```

The links Edit and Delete appear after the usernames when the user views the user list in the product. If you click on Edit, a form appears allowing you to edit the details for that user. If you click the Change User button on the edit form, this method is called and the data is changed.

The editWebsiteUser method takes the same arguments as addNewWebsiteUser().

The User folder has the method changeUser() for changing a user; this method is used with the User folder acl_users, as follows:

```
self.acl_users.changeUser(name,pwd,confirm,roles,domains)
```

# 15.4.2.12 The deleteWebsiteUser Method

Now we need another method that allows authenticated users to delete users. As you know, authenticated users have access to a list of users in acl_users and by clicking on a link, they can edit or delete that user. The link for deleting a user calls the method deleteWebsiteUser() (shown in Listing 15.14) and transfers the user's name to be deleted as a string. When you click Delete, the user is deleted immediately.

Listing 15-6: The method deleteWebsiteUser() for the Website product

```
# Allow users with the "Manage users" permission access to this method
security.declareProtected('Manage users', 'deleteWebsiteUser')
```

```
def deleteWebsiteUser(self, name):
```