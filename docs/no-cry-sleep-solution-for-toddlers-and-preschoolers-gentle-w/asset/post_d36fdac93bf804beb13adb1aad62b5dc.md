
| Directive | Description |
|---|---|
| Anonymous_Authoritative on | off | When on, there is no fall-through to other authorization methods. |
| AuthDBMUserFile filename | DBM file containing the list of users and passwords for user authentication. |
| AuthName auth-domain | The authorization realm for a directory. A realm is given to the client so the user knows which username and password to send. |
| AuthType type | Type of user authentication for a directory. Only Basic and Digest are currently implemented. |
| require entity-name entity entity ... | Selects the authenticated users that can access a directory. entity-name is either the user or group, followed by a list of users or groups. require user userID userID ... require group group-name group-name ... |
| AuthUserFile filename | Sets the name of the file with the list of users and passwords for user authentication. |

## TABLE 22-9 Authentication Directives (continued)

To apply authentication directives to a certain directory, you place those directives within either a Directory block or the directory's .htaccess file. You use the require directive to determine what users can access the directory. You can list particular users or groups. The AuthName directive provides the authentication realm to the user, the name used to identify the particular set of resources accessed by this authentication process. The AuthType directive specifies the type of authentication, such as basic or digest. A require directive requires also AuthType, AuthName, and directives specifying the locations of group and user authentication files. In the following example, only the users george, robert, and mark are allowed access to the newpics directory:

```
<Directory /var/www/html/newpics>
  AuthType Basic
  AuthName Newpics
  AuthUserFile /web/users
  AuthGroupFile /web/groups
  <Limit GET POST>
    require users george robert mark
  </Limit>
</Directory>
```

The next example allows group access by administrators to the CGI directory:

```
<Directory /var/www/html/cgi-bin
  AuthType Basic
  AuthName CGI
  AuthGroupFile /web/groups
```

```
<Limit GET POST>
require groups admin
</Limit>
</Directory>
```

To set up anonymous access for a directory, place the Anonymous directive with the user anonymous as its argument in the directory’s Directory block or .htaccess file. You can also use the Anonymous directive to provide access to particular users without requiring passwords from them.

Apache maintains its own user and group authentication files specifying what users and groups are allowed to which directories. These files are normally simple flat files, such as your system’s password and group files. They can become large, however, possibly slowing down authentication lookups. As an alternative, many sites have used database management files in place of these flat files. Database methods are then used to access the files, providing a faster response time. Apache has directives for specifying the authentication files, depending on the type of file you are using. The AuthUserFile and AuthGroupFile directives are used to specify the location of authentication files that have a standard flat file format. The AuthDBUserFile and AuthDBGroupFile directives are used for DB database files, and the AuthDBMUserFile and AuthDBMGroupFile are used for DBMG database files.

The programs htdigest, htpasswd, and dbmmanage are tools provided with the Apache software package for creating and maintaining user authentication files, which are user password files listing users who have access to specific directories or resources on your Web site. htdigest and htpasswd manage a simple flat file of user authentication records, whereas dbmmanage uses a more complex database management format. If your user list is extensive, you may want to use a database file for fast lookups. htdigest takes as its arguments the authentication file, the realm, and the username, creating or updating the user entry. htpasswd can also employ encryption on the password. dbmmanage has an extensive set of options to add, delete, and update user entries. A variety of different database formats are used to set up such files. Three common ones are Berkeley DB2, NDBM, and GNU GDBM. dbmmanage looks for the system libraries for these formats in that order. Be careful to be consistent in using the same format for your authentication files.

## Log Files

Apache maintains logs of all requests by users to your Web site. By default, these logs include records using the Common Log Format (CLF). The record for each request takes up a line composed of several fields: host, identity check, authenticated user (for logins), the date, the request line submitted by the client, the status sent to the client, and the size of the object sent in bytes. Log file directives are listed in Table 22-10.

## Webalizer

Reports on Web logs can be generated using the Webalizer tool. Webalizer will display information on your Web site usage. When you run the webalizer command, usage reports will be placed in the /var/www/html/usage directory. Access the index page to display a page with links to monthly reports, file:/var/www/html/usage/index.html. Report configuration is specified in the /etc/webalizer.conf file. Previous summaries are kept in the /etc/webalizer.history file.
