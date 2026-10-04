# C.3 The DTML Methods for the Website Product

The following section contains the source text of the DTML files which create the Website product for each instance as well as brief descriptions of the methods. These files are stored in the public directory of the product.

# C.3.1 WebsiteUsers_list.dtml

```
<dtml-var standard_html_header>
<h2>Registered website users</h2>
<p>
<dtml-call "REQUEST.set('UL', acl_users.getUserNames())">
<ul>
<table>
<dtml-in UL>
<tr>
<td><dtml-var sequence-item></li></td>
<td>
<a href="edit_WebsiteUser?uname=dtml-var sequence-item"><font color="#0068a0">Edit</font></a> |
<a href="deleteWebsiteUser?uname=dtml-var sequence-item"><font color="#0068a0">Delete</font></a>
</td>
</dtml-in>
<tr></tr>
</table>
</ul>
</p>
<dtml-var standard_html_footer>
```

This DTML method is used to list the users which exist in the acl_users of an instance of the product. Using acl_users.getUserNames() obtain a list of existing users. This list is then processed with <dtml-in>. Each username is then displayed on the website with links for editing and deleting the user after each name. These links pass on the relevant username to the DTML method (edit_WebsiteUser) or the Python method (Delete_WebsiteUser()).

# C.3.2 edit_WebsiteUser.dtml

```
<dtml-var standard_html_header>
<h2>Edit website user</h2>
<p>
<dtml-call "REQUEST.set('uname', acl_users.getUser(['uname']))">

<form action="editWebsiteUser" method="post">
<table>
<tr>
<th align="left">Name</th>
<td><dtml-var uname><input type="hidden" name="name" value="dtml-var uname"></td>

```