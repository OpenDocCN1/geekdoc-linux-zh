
AuthName "Apache Server Bible Readers Only"
AuthType Basic
AuthUserDBFile /www/secrets/myuserdbm
require valid-user

Now Apache uses the `mod_auth_dbm` module for authentication in the directory where this configuration applies.

> **Caution** Make sure that only Apache and the owner can read the DBM file. No one but the owner of the DBM file should be able to write to it.

### mod_auth_db

If your system is not capable of using DBM, but Berkeley DB file support is available, you can use `mod_auth_db` to use DB files instead of the DBM modules for Apache. This module is not compiled in the standard Apache distribution.

Before configuring Apache with DB file based authentication module, make sure you know where the DB library files are stored on your system. For example, on a Linux system, the files are in the standard `/usr/lib` directory. If your system does not have the DB libraries, you will have to get the source code and compile DB support first. You can find DB library information at www.sleepycat.com.

After you have made sure that your system has DB libraries, you can proceed with reconfiguring and recompiling Apache. Use the `--enable-db` option with `configure` script to configure the Apache source for Berkeley DB support, and then compile and install Apache as usual.

At this point, you are ready to use the `mod_auth_db` module. This `mod_auth_db` module provides the `AuthDBUserFile`, `AuthDBGroupFile`, and `AuthDBAuthorize` directives.

#### AuthDBUserFile

The `AuthDBUserFile` directive sets the fully qualified pathname of the user DB file that contains the list of users and encrypted passwords.

- **Syntax**: AuthDBUserFile *filename*
- **Context**: Directory, per-directory access control file (`.htaccess`)
- **Override**: AuthConfig

Like its DBM counterpart, the DB user file is also keyed using the username and the value is the `crypt()`-encrypted password.

> **Caution** Always make sure your user files are kept outside the Web document tree and are only readable by Apache. No one but the owner (Apache) should have write access to these files.

#### AuthDBGroupFile

The AuthDBGroupFile directive sets the fully qualified pathname of the group DB file, which contains the list of user groups for user authentication. Like its DBM counterpart, the group file uses the username as the key and the comma-separated group list is treated as the value. There must be no whitespace within the value, and it must never contain any colons.

- **Syntax**: AuthDBGroupFile *filename*
- **Context**: Directory, per-directory access control file (.htaccess)
- **Override**: AuthConfig

If you do not prefer to use a separate group file, you can use a single DB file to provide both password and group information. The format of the file is:

DB_File_Key(username) - encrypted_password; comma_separated_group_list

where the username is the key, and the password and group lists are two fields of the value. Other data may be left in the DB file after another colon; it is ignored by the authentication module. If you use a single DB to provide both group and password information, you will have to point both AuthDBGroup and AuthDBUserFile directives to the same file.

#### AuthDBAuthoritative

When using multiple authentication schemes such as mod_db, mod_dbm, and standard mod_auth in the same directory, you can use the AuthDBAuthoritative directive to define whether mod_auth_db is the authoritative authentication scheme. The default value of the directive enables mod_auth_db to become the authoritative authentication for the directory. Thus, if the DB-based authentication fails for a particular user, the user's credentials are not passed on to a lower-level authentication scheme. When set to the Off value, the credentials of a failed authentication are passed on to the next authentication level.

- **Syntax**: AuthDBAuthoritative On | Off
- **Default setting**: AuthDBAuthoritative On
- **Context**: Directory, per-directory access control file (.htaccess)
- **Override**: AuthConfig

## Dynamic Contents Generation Modules

The modules discussed here enable Apache to run CGI scripts, SSIs, filters, and the like. Table 5-4 lists these modules.

**Table 5-4**
**Dynamic Contents Generation Module**

| Module | Purpose |
| :--- | :--- |
| *mod_cgi* | Runs CGI scripts. See Chapter 12 for details. |
| *mod_include* | SSI filter. See Chapter 13 for details. |
| *mod_actions* | Executing CGI scripts based on media type or request method. |
| *mod_ext_filter* | Filtering output with external programs. |

### mod_actions

The `mod_actions` module is compiled by default. `mod_actions` enables you to run a CGI script based on `MIME-type` or on the HTTP request method. It offers these directives.

#### Action

The `Action` directive enables you to associate an action for a specific MIME type. The action is usually a CGI script that processes the file being requested. This allows you to execute a CGI script for a given MIME type.

- **Syntax**: `Action` *MIME-type* *cgi_script*
- **Context**: Server config, virtual host, directory, per-directory access control file (`.htaccess`)
- **Override**: `FileInfo`

For example, the following directive makes Apache run the specified script whenever an HTML file is requested:

```
Action text/html /cgi-bin/somescript.pl
```

The script receives the URL and file path of the requested document via the standard `CGI_PATH_INFO` and `PATH_TRANSLATED` environment variables. This can be useful in developing filter scripts. This section discusses one such filter script.

When a text file (`.txt`) is requested via the Web, it appears on the Web browser in a less-than-desirable format, because line breaks are not translated by most Web browsers in any manner. Usually, most text files appear as a large paragraph. By using the `Action` directive, you can develop a better solution.

For a more interesting example, let’s say that you now want to develop a solution that not only displays the text files better on the Web browser, but also inserts a copyright message at the end of each text file. To accomplish this, you need to do two things. First, add the following directive in httpd.conf file:

```
Action plain/text /cgi-bin/textfilter.pl
```

Then, develop the Perl script textfilter which will display the text file the way you wish. Listing 5-1 shows one such script. You can find this script on the accompanying CD-ROM in the Scripts/Chapter 5 directory.

#### Listing 5-1: textfilter.pl

```perl
#!/usr/bin/perl
#
# Script: textfilter.pl
#
# Purpose: This filter script converts plain text files
#         into an HTML document but keeps the text layout
#         as is.
#
# Copyright (c) 2001 by Mohammed J. Kabir
#
# License: GPL
#
# The copyright message file is always stored in
# the server's document root
# directory and is called copyright.html.
my $copyright_file = $ENV{DOCUMENT_ROOT} . "/copyright.html";
# Get the requested document's path
my $path_translated = $ENV{PATH_TRANSLATED};

# Other variables needed for storing data
my $line;
my @text;
my @html;

# Store the path info and the file name of requested doc in an
array
@filename = split(/\/\/.{$path_translated};

# Because HTML tags are used to display the text file,
# lets print the text/html content header.
print "Content-type: text/html\n\n";

# Read the document requested and store the data
# in @text array variable
@text = &readFile($path_translated);
# Now print the following HTML document tags.
# These tags will be sent before the actual document content
#
print <<HEAD;
<HTML>
<HEAD><TITLE>$filename[-1] </TITLE> </HEAD>
<BODY BGCOLOR="white">
<BLOCKQUOTE>
<PRE>
HEAD
# Now print each line stored in the @text array
# (that is, the content of the document requested)
#
foreach $line (@text) { print $line; }
# Now read the copyright file and store the content
# in the @html array variable
#
@html = &readFile($copyright_file);
# Print each line stored in the @html array (that is,
# the content of the copyright message file)
#
foreach $line (@html){ print $line; }
# Exit the filter
exit 0;

sub readFile {
#
# Subroutine: readFile
# Purpose: Reads a file if it exists or else prints
# an error message and exits script
#
# Get the name of the passed file name and store
# it in variable $file
my $file = shift;
# Local buffer variable
my @buffer;
# If the file exists, open it and read all the
# lines into the @buffer array variable
if(-e $file) {
open(FP,$file) || die "Can not open $file:";
while(<FP>){
```
