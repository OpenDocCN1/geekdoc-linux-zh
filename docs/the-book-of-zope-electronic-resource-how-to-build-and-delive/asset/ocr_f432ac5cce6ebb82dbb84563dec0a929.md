| Permission | Roles | | | |
| --- | --- | --- | --- | --- |
| Acquire permission settings? | Anonymous | Manager | Owner | WebsiteUser |
| Access contents information | 🅿 | 🅿 | 🅿 | ☑ |
| Change HTML Methods | 🅿 | 🅿 | 🅿 | ☑ |
| Change cache settings | 🅿 | 🅿 | 🅿 | ☑ |
| Change permissions | 🅿 | 🅿 | 🅿 | ☑ |
| Change proxy roles | 🅿 | 🅿 | 🅿 | ☑ |
| Delete objects | 🅿 | 🅿 | 🅿 | ☑ |
| FTP access | 🅿 | 🅿 | 🅿 | ☑ |
| Manage properties | 🅿 | 🅿 | 🅿 | ☑ |
| Take ownership | 🅿 | 🅿 | 🅿 | ☑ |
| Undo | 🅿 | 🅿 | 🅿 | ☑ |
| View | 🅿 | 🅿 | 🅿 | ☑ |
| View History | 🅿 | 🅿 | 🅿 | ☑ |
| View management screens | 🅿 | 🅿 | 🅿 | ☑ |

Save Changes
Figure 5-5: Permissions assignments for the DTML content login_html

To be sure that, after we submit the form (addWebsiteForm), the browser returns to the contents screen of the folder where the instance was created, add the following lines:

```
if REQUEST is not None:
    return self.manage_main(self, REQUEST)
```

# 15.4.4.2 Completed addWebsite Constructor Method
Here is the complete method code listing at a glance:

```
def manage_addwebsite(self, id, title, REQUEST=None):
    """Add a new Website"""
    instance=Website()
    instance.id=id
    instance.title=title
    user_folder=UserFolder())
    instance.setObject('acl_users', user_folder)
    instance.addRole('WebsiteUser')
    p_list = ['Access contents information',
             'Manager users', 'View']
    for permission in p_list:
        p=Permission(permission, '',instance)
        p.setRole('WebsiteUser', permission in p_list)
    self._setObject(id, instance)
    addDocsToFolder(instance, Website_pages)
    old_permissions = self.permission_settings()
    new_permissions = []
```