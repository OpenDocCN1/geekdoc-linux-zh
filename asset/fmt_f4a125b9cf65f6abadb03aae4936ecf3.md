
Apache 2.0 及更高版本现在使用一种新的内部架构，支持多处理模块（MPMs）。这些模块由服务器用于各种任务，例如网络和进程管理，并编译到 Apache 中。MPMs 使 Apache 能够在更广泛的计算机平台上工作得更好，并且可以帮助提高服务器的稳定性、兼容性和可扩展性。

Apache 在任何时候只能使用一个 MPM。这些模块与随 Apache 包含的基础集合不同（参见本章后面的“Apache Modules”部分），但用于实现设置、限制或其他服务器操作。每个模块反过来又支持许多额外的设置，称为指令，可进一步细化服务器操作。

The internal MPM modules relevant for Linux include

- `mpm_common`—A set of 20 directives common to all MPM modules
- `prefork`—A nonthreaded, preforking web server that works similar to earlier (1.3) versions of Apache
- `worker`—Provides a hybrid multiprocess multithreaded server

MPM enables Apache to be used on equipment with fewer resources yet still handle massive numbers of hits and provide stable service. The `worker` module provides directives to control how many simultaneous connections your server can handle.

> NOTE
> Other MPMs are available for Apache related to other platforms, such as `mpm_netware` for NetWare hosts and `mpm_winnt` for NT platforms. An MPM named `perchild`, which provides user ID assignment to selected daemon processes, is under development. For more information, browse to the Apache Software Foundation's home page at http://www.apache.org.

## Using .htaccess Configuration Files

Apache also supports special configuration files, known as `.htaccess` files. Almost any directive that appears in `apache2.conf` can appear in a `.htaccess` file. This file, specified in the `AccessFileName` directive in `apache2.conf` sets configurations on a per-directory (usually in a user directory) basis. As the system administrator, you can specify both the name of this file and which of the server configurations can be overridden by the contents of this file. This is especially useful for sites in which there are multiple content providers and you want to control what these people can do with their space.

To limit which server configurations the `.htaccess` files can override, use the `AllowOverride` directive. `AllowOverride` can be set globally or per directory. For example, in your `apache2.conf` file, you could use the following:

```
# Each directory to which Apache has access can be configured with respect
# to which services and features are allowed and/or disabled in that
# directory (and its subdirectories).
#
# First, we configure the "default" to be a very restrictive set of
# permissions.
#
<Directory />
    Options FollowSymLinks
    AllowOverride None
</Directory>
```

## Options Directives

To configure which configuration options are available to Apache by default, you must use the `Options` directive. `Options` can be `None`; `All`; or any combination of `Indexes`, `Includes`, `FollowSymLinks`, `ExecCGI`, and `Multiviews`. `Multiviews` isn't included in `All` and must be specified explicitly. These options are explained in Table 20.2.

### TABLE 20.2 Switches Used by the Options Directive

| Switch | Description |
|---|---|
| `None` | None of the available options are enabled for this directory. |
| `All` | All the available options, except for `Multiviews`, are enabled for this directory. |
| `Indexes` | In the absence of an `index.html` file or another `DirectoryIndex` file, a listing of the files in the directory is generated as an HTML page for display to the user. |
| `Includes` | Server-side includes (SSIs) are permitted in this directory. This can also be written as `IncludesNoExec` if you want to allow includes but don't want to allow the exec option in them. For security reasons, this is usually a good idea in directories over which you don't have complete control, such as `UserDir` directories. |
| `FollowSymLinks` | Allows access to directories that are symbolically linked to a document directory. You should never set this globally for the whole server and only rarely for individual directories. This option is a potential security risk because it allows web users to escape from the document directory and could potentially allow them access to portions of your file system where you really don't want people poking around. |
