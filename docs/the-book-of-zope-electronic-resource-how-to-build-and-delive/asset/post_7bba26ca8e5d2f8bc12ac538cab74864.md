
## Listing 6-2: DTML Document Form "user_create_form"

```
<dml-var standard_html_header>
<h2>Create a new user</h2>
<p>
Please complete the following table to create a new user:
</p>
<FORM ACTION="create_user" METHOD=POST>
<table>
<tr>
<th>Id (Name of User):</th>
<td><input type="text" size=20 name="name"></td>
</tr>
<tr>
<th>Password:</th>
<td><input type="password" size=10 name="password"></td>
</tr>
<tr>
<th>Confirm Password:</th>
<td><input type="password" size=10 name="confirm"></td>
</tr>
<tr>
<th>Domains:</th>
<td><input type="text" size=20 name="domains:tokens"></td>
</tr>
<tr>
<td><input type="submit" value="Create user"></td>
<td><input type="reset"></td>
</tr>
</table>
</FORM>
<dml-var standard_html_footer>
```

The form in this DTML document refers to another object, user_create (using the ACTION attribute of the Form tag), which is a DTML method that creates the user. It has the following code:

## Listing 6-3: DTML Method "user_create"

```
<dml-var standard_html_header>
<h2>dml-var_title_or_id</h2>
<dml-call expr="REQUEST.set('roles', ['Friends'])">
<dml-call expr="acl_users.manage_users('Add', REQUEST, RESPONSE)">
The user dml-var name="name" has been added.
<dml-var standard_html_footer>
```

When add_user_form is submitted, Zope puts the values supplied on the form into the REQUEST variables: name, password, confirm, and domains. We do not want the user to be able to select a role other than Friends, so we put that value into REQUEST manually using REQUEST.set in create_user.

## 6.3.2 Problems When Creating Users in HTML

Table 6-1 shows several reasons that an attempt to create a new user might not work.

## Table 6-1: Possible Problems with Creating Users

| Problem | Result |
|---|---|
| A user with this name already exists. | The new user is not created; the existing user is not changed. |
| Password and Confirm do not match. | The new user is not created. |
| There is no User Folder in the current folder | The new user is created in the next highest User Folder with the id acl_users. |

In each of these three cases, the manage_users call either does or does not work as desired. The problem is that no message is returned and, as a result, you do not notice that the user was not created. To solve this problem, create users with Zope's Add User form (addUser.html) in the directory /lib/python/Access/Control/(html) so that error messages will be displayed if any of the problems above occur.

You can change the layout of addUser.html to suit your own requirements, because as designed it works only in the Zope management screen. The ACTION in the Form tag of the HTML form in acl_users/manage_users must be changed because you will be creating a custom DTML method to create users not contained in the acl_users User Folder (User Folders can only contain User objects). The DTML method you create will call the Zope Folder's built-in Python method manage_users.

One problem with using the addUser.html form is, once the user has been added, the Contents view of the User Folder (acl_users) appears because manage_users() redirects the browser to this page. Visitors to the website as users with the role Friend are not authorized to access the Zope Management screen. If a visitor attempts to access the Contents view of the User Folder, Zope recognizes the current visitor as unauthorized and displays the login window.

## 6.3.3 Changing Users in DTML

You can use the command acl_users.manage_users() to change a user in much the same way as you would create a user. Following is an example of how to use DTML to see whether a user already exists in the current acl_users folder and, if, how to change that user:

## Listing 6-4: Changing a User after Checking

```
1:    <html-var standard.html_header>
2:    <html-call expr='REQUEST.set('name', 'Billy')'>
3:    <html-call expr='REQUEST.set('password', 'hello')'>
4:    <html-call expr='REQUEST.set('confirm', 'hello')'>
5:    <html-call expr='REQUEST.set('domains', [])'>
6:    <html-call expr='REQUEST.set('roles', ['Manager', 'Owner'])'>
7:    <html-if expr='acl_users.getUser(REQUEST.name)'>
8:        <html-call expr='acl_users.manage_users('Change', REQUEST, RESPONSE)'>
9:        <p>User dt-var name="name" updated.</p>
10:   <html-else>
11:       <p>User dt-var name="name" does not exist.</p>
12:   </html-if>
13:   <html-var standard.html_footer>
```

Listing 6-4 uses REQUEST.set (Lines 2 through 6) to create variables containing the user's updated information. This data could also be passed from a form (as in Listing 6.3), in which case you could omit these calls.

Next, dhtml-if (Line 6) determines if the specified username exists by calling the getUser method of the acl_users User Folder and passing the name of the user in REQUEST.name. If that user exists, it is returned by the method, and the expression is evaluated as true. If the user does not exist, getUser returns None, which is evaluated as false.

If our user exists (the dhtml-if expression is true), we call the acl_users.manage_users method (Line 7), passing the value 'Change' as its argument. This tells the method we want to change an existing user (as opposed to adding one as in the previous example). After this call, a message is returned indicating that the user was updated (Line 8).

If our user does not exist (the dhtml-if expression is true),

## 6.3.4 Deleting Users in DTML

To delete users, set the argument for manage_users to Delete. You can delete one or more users simultaneously, as the example "Changing Users" above used the method.

## Listing 6-5: Deleting or More Users

```
<html-call expr='REQUEST.set('name', ['Friends'])'>
<html-call expr='acl_users.manage_users('Delete', REQUEST, RESPONSE)
```

As in the example "Changing Users", the acl_users.manage_users method is used. Figure 6-1: To delete a user folder, the following examples are possible:

1. acl_users.getUser()
2. test_folder.acl_users.getUser()
3. test_folder.subfolder.acl_users.getUser()
4. second_folder.acl_users.getUser()

## 6.3.5 User Folder Methods

Table 6-2 lists available user folder methods.

## Table 6-2: User Folder Methods

| Method | Description | Example |
|---|---|---|
| getUser(name) | Returns the user object with the name specified or if no user that name exists. | "getUser('Casey')" |
| getUserById([id,]) | Similar to getUser, except it returns an optional default value (or raises an error) if the user does not exist. | "getUserById('Duncan')" |
| getUsers() | Returns a list of all user objects in the user folder. | "getUsers()" |
| getUserNames(user_name()) | Returns a list of all the names of the users in the user folder. | "getUserNames()/user_names()" |

Listing 6-6 shows a simple query that checks to see whether the user currently logged in exists in the User Folder.

## Listing 6-6: Checking Whether a User Exists in the Current User Folder

```
<dt-if "acl_users.getUser(AUTHENTICATED_USER.getUsername())">
Currently logged in user exists in User Folder.
<dt-else>
logged in user does not exist in User Folder.
</dt-if>
```

AUTHENTICATED_USER.getUsername() returns the name of the user currently logged on.

To check a user in a folder other than the current User Folder, you must access the relevant User Folder through the also folder(s) and/or subfolder(s).

```
<dt-var "Folder.acl_users.getUser(AUTHENTICATED_USER.getUsername())"
<dt-var "Folder.subfolder.acl_users.getUser(AUTHENTICATED_USER.getUsername())">
```

Section 8.2.1 documents additional methods available in AUTHENTICATED_USER.

# Summary

This chapter covered the basics of Zope's security system and management using roles and permissions. You have learned about the various objects and attributes Zope uses for security and how to affect them through the management screen and through DTML. Chapter 7 will look at roles and permissions in more depth.
