In addition to the settings that are configured using the `Options` directive, many other directives can be used on a per directory basis. These include directives for the following:

+   - File content handling
+   - File indexing options
+   - Error response settings
+   - Authorization and access control (security) settings

In fact, although many of the directives that have been discussed so far have been presented in the context of the server configuration files, many are more appropriately placed in a per directory area of `httpd.conf`. If you need to determine whether a particular directive can be applied on a per directory basis, see the online documentation. For each directive, the documentation indicates the contexts in which the directive can be used.

# ### Defining Options for a Specific Part of the Document Tree

Options that apply to a specific part of the filesystem are defined by placing their directives within a section of the `httpd.conf` file or in a special file called `.htaccess`.

A section in the `httpd.conf` file is defined by an opening and closing directive. For example, to apply certain options to only the objects in the directory `/usr/local/apache/icons`, you can declare a section in `httpd.conf` such as the following:

```
```apache
<Directory /usr/local/apache/icons>
    Options Indexes
    IndexOptions FancyIndexing SuppressDescription SuppressSize
</Directory>
```
```

Several different section directives can indicate the set of objects to which they apply based on different criteria:

+   - **`<Directory>`**—Matches objects based on the directory where they reside.
+   - **`<Files>`**—Matches objects based on their filenames.
+   - **`<Location>`**—Matches objects based on the URL path used to access them.

Each of these directives is used by placing the target path or filename inside the angle brackets. Then the desired directives, which apply to the indicated object set, are declared, followed by a matching close-section directive (`</Directory>`, `</Files>`, and `</Location>`, respectively).

You can also use the directives `<DirectoryMatch>`, `<FilesMatch>`, and `<LocationMatch>`, which take a regular expression as their argument instead of a simple string; this results in even more flexibility in defining a target object set. A few examples follow:

+   - **`<Directory /usr/local/apache/icons>`**—Declares a section for specifying settings in the icons directory.
+   - **`<FilesMatch ".*\.txt$">`**—Declares a section that applies to files that end in `.txt`.

![](bbox=[0.929, 0.578, 0.999, 0.694])