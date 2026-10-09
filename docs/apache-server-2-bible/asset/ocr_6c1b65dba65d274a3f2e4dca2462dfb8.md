For example, if you plan to use DBM files, change the line to:

```
BEGIN ( $AnyDBM_File::ISA -qw( GDBM_File , DB_File, NDBM_File) )
```

To find out what options the script provides, run it as follows:

```
./dbmanage
```

This shows you a syntax line with all the possible options. To create a new DBM file called /www/secrets/myuserdbm by adding a user named reader, enter the following command:

```
./dbmanage /www/secrets/myuserdbm adduser reader
```

The script will ask you to enter (and reenter) a password for the user reader. After you have done so, it will add the username and encrypted password to the myuserdbm DBM file. Do not use the add option to add a user because it does not encrypt the password. To see a list of all users in a DBM file, use the following script:

```
./dbmanage /path/to/your/dbmfile view
```

After you have recompiled Apache with DBM support, you can use the module mod_auth_dbm to provide DBM-based Basic HTTP authentication. Note that for Berkeley DB you have to use mod_auth_db instead of mod_auth_dbm.

The mod_auth_dbm module provides the directives AuthDBMUserFile, AuthDBMGroupFile, and AuthDBMAuthoritative. Let's take a look at each of these directives and some examples that use the mod_auth_dbm module.

# AuthDBMUserFile

The AuthDBMUserFile directive sets the fully qualified pathname of a DBM file to be used as the user file for DBM authentication. The file contains a key-value pair per record, in which the username is the key and the crypt()-encrypted password is the value. Note that each field in the record is separated by a colon, and arbitrary data can be appended after the initial username and password fields.

**Syntax:** AuthDBMUserFile filename

**Context:** Directory, per-directory access control file (.htaccess)

**Override:** AuthConfig

![](bbox=[0.13, 0.83, 0.19, 0.88])

> Never store user database files inside your Web document tree because someone might download the entire user database and abuse it.

# AuthDBMGroupFile

The AuthDBMGroupFile directive sets the fully qualified pathname of the group file that contains the list of user groups. Each record in the file is a key-value pair, in