```
####################################################
## Changing the permission setting of login_html ##
## for the password check ##
####################################################
```

```
old_permissions = self.permission_settings()
new_permissions = []
permissions_for_WebsiteUsers = []
for item in old_permissions:
    if item['name']=='View':
        permissions_for_WebsiteUsers.append(item['name'])
    else:
        new_permissions.append(item['name'])
instance.login_html.manage_acquiredPermissions(new_permissions)
instance.login_html.manage_role('WebsiteUser', permissions_for_WebsiteUsers)
```

IF REQUEST is not Not:
    return self.manage_main(self, REQUEST)

# C.2.1 addWebsiteForm.dtml

```
<dtml-var standard_html_header>
<form action="manage_addwebsite" method="post">
<h2>Add a new Website</h2>
<p>The product Website is a folderish object with several DTML Methods
as well as a User Folder containing a user already created.</p>
<table>
<tr>
<th></th>
<td><input type="text" name="id" size="20"></td>
</tr>
<th><em>Title:</em></th>
<td><input type="text" name="title" size="20"></td>
</tr>
<td></td></tr>
<td><input type="submit" value="Add"></td>
</table>
</form>
<dtml-var standard_html_footer>
```

addWebsiteForm.dtml is the constructor form for the Website class. It loaded
ast stored as a DTMLFile object in the Website class. When submitted, it calls the
manage_addWebsite constructor method of the main Website module.