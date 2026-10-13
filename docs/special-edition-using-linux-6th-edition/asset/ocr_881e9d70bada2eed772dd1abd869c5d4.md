# SECTION ORDERING

There might be overlaps between the sets of files that are specified by different section directives and the .htaccess file. When this happens, the options are accumulated from the sections that apply, in the order that the sections are processed. This means that the last section that is processed determines the settings.

Sections are processed in the following order:

+   - `<Directory>` and `.htaccess` files. Within this group, sections are ordered by directory name length from shortest to longest. `.htaccess` files are processed after `<Directory>` sections for matching directories.
+   - `<DirectoryMatch>`.
+   - `<File>` and `<FileMatch>`.
+   - `<Location>` and `<LocationMatch>`.

The result of the “shortest to longest” part of the first rule is that the options for a directory apply to that directory and all its subdirectories, until another section (with a longer, and thus more specific directory path) overrides them.

In the case of duplicate entries within each category (for example, two `<Directory>` sections with the same directory name), the sections are processed in the order in which they occur in the configuration files. The configuration files are read in the following order: httpd.conf, srm.conf, and access.conf.

> **Note:** The srm.conf and access.conf files are only processed for historical reasons. Generally, all directives should be placed in httpd.conf to reduce complexity.

# ALL ABOUT LOGGING

One nice thing about the Web server is that you can configure it to provide all kinds of information about itself and the operations that it is performing, through server log files. By default, the Web server logs each request that it fulfills and each error that it encounters in the access log and the error log, respectively. However, you can create additional logs of server activity and customize the format of each log entry.

There are five basic types of logs that the Web server can produce:

+   - Transfer log
+   - Agent log
+   - Referrer log
+   - Error log
+   - Script log

Each of these logs is described in detail in the sections that follow.