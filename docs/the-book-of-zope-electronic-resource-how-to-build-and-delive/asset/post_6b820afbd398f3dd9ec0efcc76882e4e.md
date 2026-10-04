
## #7
## LOCAL ROLES AND PERMISSIONS

![](img/43a28cce5475b2f487bf455365567fb6_146_0.png)

Sometimes, you may want to give users in one role the same permissions as another; for example you might wish to give a Friend the same permissions as a Manager for one particular object (for example, a DTML document or a specific folder), in which case there is little point in assigning the user (let us call him "Egon") the role of Manager, because he will then be able to see and use the management screen for the whole of Zope. Egon should only be able to modify the folder My_Homepage. Similarly, if you give the role Friends the same permissions as Manager, all users in the Friends role will have Manager permissions for the folder My_Homepage.

### 7.1 Local Roles

It is at this point that local roles come into play. Local roles allow us to assign a different role to a user created in the acl_users folder for a specific object, to be it a folder or individual document.

### 7.1.1 Example

To give Egon the same permission as a Manager for the folder My_Homepage, we must first open the Security screen for the folder My_Homepage, shown in Figure 7-1. Notice the link local roles in the introduction text.

#### Folder at /

The listing below shows the current security settings for this item. Permissions are rows and roles. Checkboxes are used to indicate where roles are assigned. You can also assign local roles to users, which gives users extra roles in the context of this object and its subjects.

When a role is assigned to a permission, users with the given role will be able to perform tasks associated with the permission on this item. When the Acquire permission checkbox is selected the containing object's permission settings are used. The acquired permission settings may be augmented by selecting Roles for a permission in addition to selecting acquire permissions

| Permission | Anonymous | Friends | Manager | Owner |
| --- | --- | --- | --- | --- |
| Access contents information | ☐ | ☐ | ☐ | ☐ |
| Added HTTP Cache Managers | ☐ | ☐ | ☐ | ☐ |
| Add Database Methods | ☐ | ☐ | ☐ | ☐ |
| Add Documents, Images, and Files | ☐ | ☐ | ☐ | ☐ |
| Add External Methods | ☐ | ☐ | ☐ | ☐ |

Figure 7-1: Security screen with local roles link

Clicking the local roles link opens another page (Figure 7-2) that contains a list of all local roles already set up for this object. As you can see in Figure 7-2, only the local role Owner has been set for the user who created the folder My_Homepage in our example.

Figure 7-2 shows two multiple-select lists: To the left is a list of all users for whom local roles can be set, and to the right is a list of all local roles that can be used for this object.

![](img/43a28cce5475b2f487bf455365567fb6_147_0.png)

Figure 7-2: Screen for managing local roles

We now select Egon from the list of users and Manager from the list of roles. When we click on the Add button under the two lists, Egon appears in the list of set local roles (with the local role set in brackets after the name). Egon can now carry out all activities in the folder My_Homepage that could normally be carried out only by a Manager.

Say you have created a form for sending email (for example, sendEmail), a HTML method (for example, sendEmail) with the sendmail command, and a MailHost. If you want to allow only certain users (for example, Egon) to send this way, you may think that it would be a good idea to assign the local role of Manager to Egon for the DTML method sendEmail, because this DTML method contains the sendmail command. This will not, however, produce the desired results. To allow Egon to send email, he must be assigned the Manager local role in the MailHost object. Of course, this also means that he will be able to change the MailHost object—a possible drawback you should consider.

### 7.2 Proxy Roles

Proxy roles serve a purpose similar to local roles, but proxy roles are object-related whereas local roles are user-related. Proxy roles allow all users who access the object to have the same permissions, regardless of the role assigned to them.
Let's look at an example:

Suppose you have created a new DTML document index_html with the standard source code (see "Access contents information" below). To assign the proxy role as Anonymous:

- 1. Go to the Edit view of the DTML document and click the Proxy tab to call up the Proxy view, where you'll find a list of all roles that can be assigned as a proxy role for this object.
- 2. Select Anonymous from this list and click the Save Changes button.
- 3. Now go to the containing folder's Security view and deactivate acquisition for the permission Access contents information.
- 4. Save the changes to the folder's permissions.

This interrupts the acquisition chain and removes the Access contents information from the Anonymous role. However, this permission is needed to view a DTML document that contains the DTML command

```
<dtml-var id>
```

--- the standard code for a DTML document contains. If you (or any other user) now try to view your just-created DTML document, you will be unable to.

### 7.3 Permissions

Let's take a look at some of the permissions. Different roles allow different actions. The security screen shows which permissions are assigned to which role. Figure-3 shows a typical security screen for a folderish object.

![](img/43a28cce5475b2f487bf455365567fb6_149_0.png)

Figure-3: Security screen with local roles

### 7.3.1 Permissions for Non-Folderish Objects

As mentioned in 7.3, you can set many more permissions for folderish objects than for folderish ones.

#### Access contents information

This permission allows a user to view information, such as the Title or id, relating to the object for which the permission is set. Take, for example, the standard content of a DTML document, as shown in Figure 7-1. Zope automatically inserts this content into the document by default when you create a DTML document.

#### Listing 7-1: Standard Content of a DTML Document

```
<dtml-var standard_html_header>
<h2><dtml-var title_or_id></h2>
<p>
This is the <dtml-var id> Document.
</p>
<dtml-var standard_html_footer>
```

<dtml-var title_or_id> returns the Title, if there is no Title, the id of the object; <dtml-var id> returns only the id of the object.

#### Change DTML Documents/Change DTML Methods

These permissions must be set so that changes to existing DTML documents and methods can be saved. If a user lacking the appropriate permission attempts to save changes by clicking the Change button, the user is asked to enter a password. Without this password—that is, without the appropriate permission—the user can only view the source code of the DTML document or method in the Edit screen.
