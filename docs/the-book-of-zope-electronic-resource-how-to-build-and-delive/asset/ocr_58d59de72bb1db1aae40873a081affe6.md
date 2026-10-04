```
else:
self.acl_users._adduser(name, pwd, confirm, roles, domains, REQUEST)
RESPONSE.redirect('index.html')
```

The addNewWebsiteUser() method uses a built-in private method, _addUser, of the user.py module to create a new user (see Chapter 8 for more information on this). The method's arguments are shown in Table 15-3.

# Table 15-3: Data for creating a new user

| Argument | Description |
| --- | --- |
| self | Instance of the product |
| name | The user's name |
| pwd | The user's password |
| confirm | Confirm password |
| roles | Roles for the user, as a list |
| domains | Internet domains from which the user can log in (as a list) |
| REQUEST | The REQUEST object (provided by Zope) |
| RESPONSE | The RESPONSE object (provided by Zope) |

The addNewWebsiteUser() method is coded to first see whether the name already exists in the User folder (ad_users) of the folder indicated by self. It does so using the method getUser(name), which returns a user object if that name exists and None if not. Because all user object values are considered a true value in Python and None is considered false, we can check the results of getUser(name) directly with an if statement to see if the users.

If the user exists, we use MessageDialog to generate an HTML page that contains a message and an OK button. Clicking OK opens the URL specified by the action argument. The title argument indicates what should appear in the <HEAD> element of the HTML page use as the title of the page.

If the user does not exist, a call is made to the _addUser method of the User folder in the instance of the product (a built-in private method) that you can use to directly add a new user in Zope from Python. We pass to it all information about the user to be created (username, password, and so on). Once this is completed, we redirect to the home page of the Web instance (index.html).

The method addNewWebsiteUser() is now finished. If you have already created an instance of the product, any users already logged in the website can use to create new users.

> This method on its own is not enough to allow visitors to create new users. DTML methods must be created to build the website interface and, as mentioned above, to create the security model that authenticates users.