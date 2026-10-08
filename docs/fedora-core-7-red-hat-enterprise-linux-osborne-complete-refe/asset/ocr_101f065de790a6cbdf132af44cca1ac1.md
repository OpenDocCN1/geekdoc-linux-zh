```
AuthName  CGI
AuthGroupFile /web/groups
<Limit GET POST>
    require groups admin
</Limit>
s</Directory>
```

To set up anonymous access for a directory, place the **Anonymous** directive with the user anonymous as its argument in the directory’s Directory block or .htaccess file. You can also use the **Anonymous** directive to provide access to particular users without requiring passwords from them.

Apache maintains its own user and group authentication files specifying what users and groups are allowed access to which directories. These files are normally simple flat files, such as your system’s password and group files. They can become large, however, possibly slowing down authentication lookups. As an alternative, many sites have used database management files in place of these flat files. Database methods are then used to access the files, providing a faster response time. Apache has directives for specifying the authentication files, depending on the type of file you are using. The **AuthUserFile** and **AuthGroupFile** directives are used to specify the location of authentication files that have a standard flat file format. The **AuthDBUserFile** and **AuthDBGroupFile** directives are used for DB database files, and the **AuthDBMGroupFile** and **AuthDBMGroupFile** are used for DBM database files.

The programs *htdigest*, *htpasswd*, and *dbmmanage* are tools provided with the Apache software package for creating and maintaining *user authentication files*, which are user password files listing users who have access to specific directories or resources on your Web site. The *htdigest* and *htpasswd* programs manage a simple flat file of user authentication records, whereas *dbmmanage* uses a more complex database management format. If your user list is extensive, you may want to use a database file for fast lookups. *htdigest* takes as its arguments the authentication file, the realm, and the username, creating or updating the user entry. *htpasswd* can also employ encryption on the password. *dbmmanage* has an extensive set of options to add, delete, and update user entries. A variety of different database formats are used to set up such files. Three common ones are Berkeley DB2, NDBM, and GNU GDBM. *dbmmanage* looks for the system libraries for these formats in that order. Be careful to be consistent in using the same format for your authentication files.

# ## Log Files

Apache maintains logs of all requests by users to your Web site. By default, these logs include records using the Common Log Format (CLF). The record for each request takes up a line composed of several fields: host, identity check, authenticated user (for logins), the date, the request line submitted by the client, the status sent to the client, and the size of the object sent in bytes.

# ### Webalizer

Reports on Web logs can be generated using the Webalizer tool. Webalizer will display information on your Web site usage. When you run the *webalizer* command, usage reports will be placed in the */var/www/html/usage* directory. Access the index page to display a page with links to monthly reports, *file:/var/www/html/usage/index.html*. Report configuration is specified in the */etc/webalizer.conf* file. Previous summaries are kept in the */etc/webalizer.history* file.