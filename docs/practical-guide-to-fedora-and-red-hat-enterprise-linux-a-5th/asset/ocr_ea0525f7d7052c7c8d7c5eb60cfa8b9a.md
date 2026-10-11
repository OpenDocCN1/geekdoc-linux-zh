**All**: Serves content to any client.

**host**: Serves content to the client(s) specified by *host*, which can take several forms: *host* can be an FQDN, a partial domain name (such as **example.com**), an IP address, a partial IP address, or a network/netmask pair.

**var**: Serves content when the environment variable named *var* is set. You can set a variable with the SetEnvIf directive. See the Order directive (page 870) for an example.

Contexts: **directory**, **.htaccess**  
Default: none; default behavior depends on the Order directive  
Fedora/RHEL: All

AllowOverride **Specifies the classes of directives that are allowed in *.htaccess* files.**

```
*AllowOverride* All \ None \ *directive-class* [*directive-class* ...]
```

This directive specifies whether Apache read **.htaccess** files in the directory hierarchy specified by its container. If Apache does reads **.htaccess** files, this directive specifies which kinds of directives are valid within **.htaccess** files.

**None**: Ignores **.htaccess** files.

**All**: Allows all classes of directives in **.htaccess** files.

The *directive-class* is one of the following directive class identifiers:

+   * **AuthConfig**: Class of directives that control authorization (AuthName, AuthType, Require, and so on). This class is used mostly in **.htaccess** files to require a username and password to access the content. For more information refer to “Authentication Modules and **.htaccess**” on page 880.

+   * **FileInfo**: Class of directives that controls document types (DefaultType, ErrorDocument, SetHandler, and so on).

+   * **Indexes**: Class of directives relating to directory indexing (DirectoryIndex, FancyIndexing, IndexOptions, and so on).

+   * **Limit**: Class of client access directives (Allow, Deny, and Order).

+   * **Options**: Class of directives controlling directory features.

Context: **directory**  
Default: All  
Fedora/RHEL: None

Deny **Specifies which clients are not allowed to access specified content.**

```
*Deny* from All \ *host* [*host* ...] \ env=*var* [env=*var* ...]
```

This directive, which must be written as **Deny** from, denies access to a directory hierarchy to the specified clients. The directory hierarchy is specified by the container or **.htaccess** file this directive appears in. See the Order directive (page 870) for an example.