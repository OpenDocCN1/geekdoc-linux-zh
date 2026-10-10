To build Apache the easy way, run the `./configure` script in the directory just created. You can provide it with a `--prefix` argument to install it in a directory other than the default, which is `/usr/local/apache/`. Use this command:

```
`# ./configure --prefix=/preferred/directory/`
```

This generates the makefile that’s used to compile the server code.

Next, type **make** to compile the server code. After the compilation is complete, type **make install** as root to install the server. You can now configure the server via the configuration files. See the “Runtime Server Configuration Settings” section, later in this chapter, for more information.

> **TIP**
> A safer way to install a new version of Apache from source is to use the `ln` command to create symbolic links of the existing file locations (listed in the “Installing from the RPM” section earlier in this chapter) to the new locations of the files. This method is safer because the default install locations are different from those used when the RPM installs the files. Failure to use this installation method could result in your web server process not being started automatically at system startup.
> 
> Another safe way to install a new version of Apache is to first back up any important configuration directories and files (such as `/etc/httpd`) and then use the `rpm` command to remove the server. You can then install and test your new version and, if needed, easily restore your original server and settings.
> 
> It is strongly recommended that you use Fedora’s RPM version of Apache until you really know what happens at system startup. No “uninstall” option is available when installing Apache from source!

# Apache File Locations After a Build and Install

Files are placed in various subdirectories of `/usr/local/apache` (or whatever directory you specified with the `--prefix` parameter) if you build the server from source.

The following is a list of the directories used by Apache, as well as brief comments on their usage:

+   * `/usr/local/apache/conf/`—This contains several subdirectories and the Apache configuration file, `httpd.conf`. See the “Editing httpd.conf” section, later in this chapter, to learn more about configuration files.
+   * `/usr/local/apache/`—The `cgi-bin`, `icons`, and `htdocs` subdirectories contain the CGI programs, standard icons, and default HTML documents, respectively.
+   * `/usr/local/apache/bin/`—The executable programs are placed in this directory.
+   * `/usr/local/apache/logs/`—The server log files are placed in this directory. By default, there are two log files—`access_log` and `error_log`—but you can define any