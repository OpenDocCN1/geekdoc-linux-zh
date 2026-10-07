# Restrict Access

The Restrict Access page allows you to implement the security that you've created all these users and groups for.

Access control is based on several factors, including the type of access (read or write, though write is seldom implemented on Web servers), allowing or denying access to hostname or IP address, and which part of the server to set access for.

You will often see the section shown in Figure 12-10 in the Administration Server pages. This section allows you to select a part of the Web server to which configuration applies. You can select the large Browse button to help you find a directory on your Web server. The Access Control options that you select in this page then apply to the directory that you selected. The Wildcard button lets you select all files that end with .html or .cgi.

If you don't make a selection from the buttons shown in Figure 12-10, but leave them as they appear by default, with the words "The entire server," then the changes that you make, including the access control settings, will apply to every document on your Web server.

Once you have selected a part of your server for which you want to control access, using the buttons shown in Figure 12-10, you can set the access control what you want to define for that part of your Web server.

Usually, you will select Read as the Access type, then either Deny or Allow, and then use the Permissions button to enter a list of hostnames or IP addresses that are either denied or allowed access. Additional information about using allow and deny is provided in Chapter 11.

# Manage User Database

The Manage User Database page is only used if you want to have more than one user database. If the default database doesn't meet your needs fully, you can enter a new database in the New Database field and choose OK to add that database to your Web server.

Adding a new database doesn't add any users to your system or alter the security in any way. It just provides a new container that you can place user information into. Then you can grant access to those users that you add to the database.

If you want to remove a database that you've created, select that database from the drop-down list, then choose the Remove Database button. All of the users in that database are discarded. This action cannot be undone, so be very careful about using this feature!

# Import Users

If you have used another Web server, or if you want to use your Linux users as a basis for controlling access to your Web site documents, you can use this page to import a file of usernames and have each of those usernames automatically part of the Web server user database.