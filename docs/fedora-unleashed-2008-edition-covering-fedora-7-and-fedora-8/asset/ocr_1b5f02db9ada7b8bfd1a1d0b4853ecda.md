Allow Users to Compress Files
This line determines whether the user is able to use the compress command on files:

```
compress <yes;no> [<classGlob>]
```

The yes|no parameter toggles the permission on or off, and classGlob is a regular expression string that specifies one or more defined classes of users. The conversions that result from the use of this command are specified in the ftpconversions file, which contains directions on what compression or extraction command is to be used on a file with a specific extension, such as .z for the compress command, .gz for the gunzip command, and so on. See the section “Configuring FTP Server File-Conversion Actions” later in this chapter.

Assign or Deny Permission to Use tar
This line determines whether the user is able to use the tar (tape archive) command on files:

```
tar <yes;no> [<classGlob> ...]
```

The yes|no parameter toggles the permission on or off, and classGlob is a regular expression string that specifies one or more defined classes of users. Again, the conversions that result from the use of this command are specified in the ftpconversions file.

Determine What Permissions Can Apply to User-Created Upload Files
This line is a bit different from the other commands in the permission control section. The umask command determines with what permissions a user can create new files; here it is.

```
umask <yes;no> <typeList>
```

The yes|no parameter toggles based on whether a user is allowed to create a file with his default permissions when uploading a file. Like the overwrite command you read about earlier in this section, this command line is specific to uploaded files because the client machine determines how new files are created from a download.

Configure Commands Directed Toward the cpPath
This alias command allows the administrator to provide another name for a directory other than its standard name:

```
alias <string> <dir>
```

The alias line applies to only the cd command. This line is particularly useful if a popular directory is buried deep within the anonymous FTP user’s directory tree. The following is a sample entry:

```
alias linux-386 /pub/redhat/7.3/en/i386/
```