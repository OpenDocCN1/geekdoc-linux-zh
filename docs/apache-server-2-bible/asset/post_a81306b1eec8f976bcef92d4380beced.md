
## ExpiresByType

```text
ExpiresByType text/html "access plus 7 days"
ExpiresByType image/gif "modification plus 3 hours 10 minutes"
```

### ExpiresDefault

The `ExpiresDefault` directive sets the default expiration time for all documents in the context in which it is specified. For example, if this directive is specified in the virtual host context, it will only apply to the documents accessible via the virtual host. Similarly, you can specify this directive in a per-directory context, which allows all documents in that directory to expire at a specified interval. See `ExpiresByType` for details on the syntax.

- **Syntax 1:** `ExpiresDefault Mseconds | Aseconds`
- **Syntax 2:** `ExpiresDefault "base_time [plus] num Years|Months|Weeks|Days|Hours|Minutes|Seconds"`
- **Context:** Server config, virtual host, directory, per-directory access control file (`.htaccess`)
- **Override:** Indexes

Following are two examples:

```text
ExpiresDefault M3600
ExpiresDefault "access plus 2 days"
```

The first example sets the expiration time to one hour after the last modification time of the documents. The second one sets the expiration time to two days after access by the client.

## mod_cern_meta

The `mod_cern_meta` module is not compiled by default. It provides support for metainformation. This information can either be additional HTTP headers such as:

```text
Expires: Saturday, 19-May-01 12:00:00 GMT
```

or it can be any other information such as the following, where the meta information is stored in a file and appears along with the HTTP response header:

```text
Foo=Bar
```

### MetaFiles

The `MetaFiles` directive enables or disables metaheader file processing.

- **Syntax:** `MetaFiles On | Off`
- **Default setting:** `MetaFiles Off`
- **Context:** Per-directory access control file (`.htaccess`)

### MetaDir

The MetaDir directive specifies the name of the directory that stores metaheader files. For example, if you have a directory called `/www/mycompany/public/htdocs` and want to store metainformation files for that directory, you need to create a subdirectory called `.web` if you use the default value for the MetaDir directive. The `.web` directory stores metaheader files.

- **Syntax:** `MetaDir directory`
- **Default setting:** `MetaDir .web`
- **Context:** Per-directory access control file (`.htaccess`)

### MetaSuffix

The MetaSuffix directive specifies the filename extension for metainformation files. For example, if you have an HTML file called `mypage.html`, then you need to create `mypage.html.meta` (using the default value of this directive) to store your metaheaders. The `mypage.html.meta` file must reside in the directory specified by the MetaDir directive.

- **Syntax:** `MetaSuffix suffix`
- **Default setting:** `MetaSuffix .meta`
- **Context:** Per-directory access control file (`.htaccess`)

To enable Apache to send out metainformation for a directory called `/www/mycompany/public/htdocs`, you need to do the following:

1. Set the MetaFiles directive to on in the per-directory configuration file (`.htaccess`) for `/www/mycompany/public/htdocs`. You can also set the MetaDir and MetaSuffix directive in this file.
2. Create a subdirectory called `.web` (assuming you are using the default for MetaDir directive).
3. Create a text file with extension `.meta` (assuming you are using the default value for MetaSuffix directive).
4. Put all the HTTP headers that you want to supply in this file.

For example, to provide metaheaders for a file named `/www/mycompany/public/htdocs/mypage.html`, you need to create a file called `/www/mycompany/public/htdocs/.web/mypage.html.meta`. This file could include lines such as:

```text
Expires: Saturday, 19-May-01 12:00:00 GMT
Anything=Whatever
```

# Server Information and Logging Modules

The modules in this section, as shown in Table 5-9, enable you to log access, report server status and configuration information, and also to track users who are using cookies.

Table 5-9

**Server Information and Logging Modules**

| Module | Purpose |
| :--- | :--- |
| **mod_log_config** | Provides customizable access logging. See Chapter 8 for details. |
| **mod_status** | Displays status information. See Chapter 8 for details. |
| **mod_info** | Displays server configuration information. See Chapter 8 for details. |
| **mod_usertrack** | Provides user tracking by using HTTP Cookies. See Chapter 8 for details. |

## mod_log_config

This module is discussed in detail in Chapter 8. See the “Creating Log Files” section in this chapter to learn more about this module and its directives.

## mod_status

This module is discussed in detail in Chapter 8. See the “Enabling status pages with `mod_status`” section in this chapter to learn more about this module and its directives.

## mod_info

This module is discussed in detail in Chapter 8. See the “Accessing configuration information with `mod_info`” section in this chapter to learn more about this module and its directives.

## mod_usertrack

This module is discussed in detail in Chapter 8. See the “Logging Cookies” section later in this chapter to learn more about this module and its directives.

# URL Mapping Modules

The modules in this section, as shown in Table 5-10, enable you to map various URLs to specific physical directories, create complex rewriting rules, aliases, and automate virtual host URLs to physical directory mappings.

Table 5-10

**URL Mapping Modules**

| Module | Purpose |
| :--- | :--- |
| `mod_userdir` | Allows you to access personal Web sites stored in user home directories. |
| `mod_rewrite` | URL rewriting rules are created using this module. See Chapter 9 for details. |
| `mod_alias` | To map different parts of the host filesystem in the document tree and for URL redirection. |
| `mod_speling` | Automatic correction of minor typos in URLs. |
| `mod_vhost_alias` | Support for dynamically configured mass virtual hosting. |

## mod_userdir

The `mod_userdir` module enables Apache to enable user-specific Web directories that are accessible via `http://your_server_name/~username`. If you do not plan on supporting such Web sites, you do not need this module.

The UserDir directive (the only directive for this module) enables you to set the directory that Apache should consider as the document root for the user's Web site.

- **Syntax:** `UserDir directory_filename`
- **Default setting:** `UserDir public_html`
- **Context:** Server config, virtual host

For example, if you keep the default value, whenever Apache notices a `~username` path after the server name in the requesting URL, it translates the `~username` to `user_home_directory/public_html`. If user home directories are stored in `/home`, the translated path is `/home/username/public_html`.

> **Caution** You should add `UserDir disabled root` to disable the capability to set this directive to point to the root directory.

The directory name that you set with this directive must be accessible by the Web server. In other words, if `/home/username` is the home directory and you leave `UserDir` set to `public_html`, then `/home/username/public_html` must be accessible by the Web server. In fact, Apache will also require read and execute access to both the `/home` and the `/home/username` directories. Some security-conscious system administrators do not like the idea of creating a Web directory in a user's home directory, so you can set the `UserDir` to a different path such as:

```text
UserDir /www/users
```

Now when `http://your_server_name/~username` is requested, Apache will translate this request to `/www/users/username`. This way you can keep a user's Web files outside the home directory (`/home/username`) by creating a new top directory in which you have to create a directory for each user. Remember to ensure that Apache has read and execute access to each of these directories.

## mod_alias

The `mod_alias` module is compiled by default in Apache. It provides various directives that can be used to map one part of the server's file system to another, or even to perform URL redirection services.

### Alias

The `Alias` directive enables you to map a path to anywhere in your system's file system.

- **Syntax:** `Alias URL-path path`
- **Context:** Server config, virtual host

For example, the following directive maps `/data/` to `/web/data/`; therefore, when a request such as `http://www.yoursite.com/data/`

```text
Alias /data/ "/web/data/"
```

`http://data/datafile.cvs` is received, the file called `/web/data/datafile.cvs` is returned.

> **Caution:** The aliased path does not have to reside inside your document root tree, so be careful when you create aliases—you might accidentally reveal some part of your file system to the entire world.

> **Note:** If you use a trailing `/` (slash) in defining an alias, the requests that are capable of accessing the aliased directory also need to contain a trailing `/`.
