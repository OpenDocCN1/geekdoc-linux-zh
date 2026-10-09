
**NameWidth=***n***: Sets the width of the filename column to *n* characters. Use * in place of *n* to accommodate the widest filename.

**ScanHTMLTitles**: Extracts and displays titles from HTML documents. Use only with FancyIndexing. Not normally used because it is CPU and disk intensive.

**SuppressColumnSorting**: Suppresses clickable column headings that can be used for sorting columns. Use only with FancyIndexing.

**SuppressDescription**: Suppresses file descriptions. Use only with FancyIndexing.

**SuppressHTMLPreamble**: Suppresses the contents of the file specified by the Header-Name directive, even if that file exists.

**SuppressIcon**: Suppresses icons. Use only with FancyIndexing.

**SuppressLastModified**: Suppresses the modification date. Use only with FancyIndexing.

**SuppressRules**: Suppresses horizontal lines. Use only with FancyIndexing.

**SuppressSize**: Suppresses file sizes. Use only with FancyIndexing.

**VersionSort**: Sorts version numbers (in filenames) in a natural way; character strings, except for substrings of digits, are not affected.

As an example, suppose a client requests a URI that points to a directory (such as `http://www.example.com/support/`) and none of the files specified by the Directory-Index directive (page 914) is present in that directory. If the directory hierarchy is controlled by a .htaccess file and AllowOverride (page 930) has been set to allow indexes, then Apache displays a directory listing according to the options specified by this directive.

When this directive appears more than once within a directory, Apache merges the options from the directives. Use `+` and `-` to merge IndexOptions options with options from higher-level directories. (Unless you use `+` or `-` with all options, Apache discards any options set in higher-level directories.) For example, the following directives and containers set the options for `/custsup/download` to VersionSort; Apache discards FancyIndexing and IgnoreCase in the download directory because there is no `+` or `-` before VersionSort in the second `<Directory>` container:

```apache
<Directory /custsup>
    IndexOptions FancyIndexing
    IndexOptions IgnoreCase
</Directory>

<Directory /custsup/download>
    IndexOptions VersionSort
</Directory>
```

Because `+` appears before VersionSort, the directives and containers on the next page set the options for `/custsup/download` to FancyIndexing, IgnoreCase, and VersionSort.

```apache
<Directory /custsup>
  IndexOptions FancyIndexing
  IndexOptions IgnoreCase
</Directory>

<Directory /custsup/download>
  IndexOptions +VersionSort
</Directory>
```

Contexts: server config, virtual host, directory, .htaccess
Specify in httpd.conf
Default: none; lists only filenames
Ubuntu: FancyIndexing VersionSort HTMLTable NameWidth=* DescriptionWidth=* Charset=UTF-8

## **ServerRoot**

Specifies the root directory for server files (not content).

```apache
ServerRoot directory
```

where *directory* specifies the pathname of the root directory for the files that make up the server. Apache prepends *directory* to relative pathnames in httpd.conf. This directive does not specify the location of the content that Apache serves; the DocumentRoot directive (page 913) performs that function. Do not change this value unless you move the server files.

Context: server config
Specify in httpd.conf
Default: /usr/local/apache
Ubuntu: /etc/apache2

## **ServerTokens**

Specifies the server information that Apache returns to a client.

```apache
ServerTokens Prod | Major | Minor | Min | OS | Full
```

**Prod**: Returns the product name: Apache. Also ProductOnly.

**Major**: Returns the major release number of the server: Apache/2.

**Minor**: Returns the major and minor release numbers of the server: Apache/2.2.

**Min**: Returns the complete version: Apache/2.2.4. Also *Minimal*.

**OS**: Returns the name of the operating system and the complete version: Apache/2.2.4 (Ubuntu). Provides less information that might help a malicious user than Full does.

**Full**: Same as OS, except that Full also sends the names and versions of non-ASF modules: Apache/2.2.4 (Ubuntu) PHP/5.1.2.

Unless you want clients to know the details of the software you are running, set ServerTokens to reveal as little as possible.

Context: server config
Specify in httpd.conf
Default: Full
Ubuntu: Full

## ServerSignature

*Adds a line to server-generated pages.*

```apache
ServerSignature On | Off | Email
```

**On:** Turns the signature line on. The signature line contains the server version as specified by the ServerTokens directive (discussed on the preceding page) and the name specified by the `<VirtualHost>` container (page 918).

**Off:** Turns the signature line off.

**Email:** To the signature line, adds a mailto: link to the server email address. This option produces output that can attract spam. See ServerAdmin (page 912) for information on specifying an email address.

Contexts: server config, virtual host, directory, .htaccess
Specify in httpd.conf or sites-available/*
Default: Off
Ubuntu: On

### CONFIGURATION DIRECTIVES

## Group

*Sets the GID of the processes that run the servers.*

```apache
Group #groupid | groupname
```

where `#groupid` is a GID value, preceded by `#`, and `groupname` is the name of a group. The processes (servers) that Apache spawns are run as the group specified by this directive. See the User directive (page 929) for more information.

Context: server config
Specify in httpd.conf
Default: #1
Ubuntu: www-data

## Include

*Loads directives from files.*

```apache
Include filename | directory
```

where *filename* is the relative pathname of a file that contains directives. Apache prepends ServerRoot (page 926) to *filename*. The directives in *filename* are included in the file holding this directive at the location of the directive. Because *filename* can include wildcards, it can specify more than one file.

The *directory* is the relative pathname that specifies the root of a directory hierarchy that holds files containing directives. Apache prepends ServerRoot to *directory*. The directives in ordinary files in this hierarchy are included in the file holding this directive at the location of the directive. The *directory* can include wildcards.

Ubuntu Linux categorizes and splits Apache configuration information into files and directories related to virtual hosts, server configuration, ports, modules, and miscellaneous configuration options. These files are incorporated into the main apache2.conf file using Include directives; see page 906 for more information.

Contexts: **server config, virtual host, directory**
Specify anywhere
Default: none
Ubuntu:
- /etc/apache2/mods-enabled/*.load
- /etc/apache2/mods-enabled/*.conf
- /etc/apache2/httpd.conf
- /etc/apache2/ports.conf
- /etc/apache2/conf.d/
- /etc/apache2/sites-enabled/

## LoadModule

*Loads a module.*

```apache
LoadModule module filename
```

where *module* is the name of an external DSO module and *filename* is the relative pathname of the named module. Apache prepends ServerRoot (page 926) to *filename* and loads the external module specified by this directive. Use `a2enmod` (page 905) to enable modules. For more information refer to “Modules” on page 941.

Context: **server config**
Specify in **mods-available/*.load**
Default: none; nothing is loaded by default if this directive is omitted
Ubuntu: see the *.load files in the **mods-enabled** directory

## Options

*Controls server features by directory.*

```apache
Options [±]option […]
```

This directive controls which server features are enabled for a directory hierarchy. The directory hierarchy is specified by the container this directive appears in. A **+** or the absence of a **+** turns an option on, and a **-** turns it off.
The *option* may be one of the following:

- **None**—None of the features this directive can control are enabled.
- **All**—All of the features this directive can control are enabled, except for MultiViews, which you must explicitly enable.
- **ExecCGI**—Apache can execute CGI scripts (page 942).
- **FollowSymLinks**—Apache follows symbolic links.
- **Includes**—Permits SSIs (server-side includes). SSIs are containers embedded in HTML pages that are evaluated on the server before the content is passed to the client.
- **IncludesNOEXEC**—The same as Includes but disables the #exec and #exec cgi commands that are part of SSIs. Does *not* prevent the #include command from referencing CGI scripts.
- **Indexes**—Generates a directory listing if DirectoryIndex (page 914) is not set.
