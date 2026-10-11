Web pages that Apache serves, this directory can house the **usage** directory, which holds **webalizer** (page 881) output.

.htaccess files A **.htaccess** file contains configuration directives and can appear in any directory in the document root hierarchy. The location of a **.htaccess** file is critical: The directives in a **.htaccess** file apply to all files in the hierarchy rooted at the directory that holds the **.htaccess** file. You must use the AllowOverride directive (page 869) to cause Apache to examine **.htaccess** files. Based on the Fedora/RHEL **httpd.conf** file, Apache does not answer requests for files whose names start with **.ht**, so clients cannot read **.htaccess** files.

# ## CONFIGURATION DIRECTIVES

*Configuration directives*, or simply *directives*, are lines in a configuration file that control some aspect of how Apache functions. A configuration directive is composed of a keyword followed by one or more arguments (values) separated by SPACES. For example, the following configuration directive sets **Timeout** to 300 (seconds):

```
```
Timeout  300
```
```

You must enclose arguments that contain SPACES within double quotation marks. Keywords are not case sensitive, but arguments (pathnames, filenames, and so on) often are.

httpd.conf The most important file that holds Apache configuration directives is, by default, **/etc/httpd/conf/httpd.conf**. This file holds global directives that affect all content served by Apache. An Include directive (page 866) within **httpd.conf** can incorporate the contents of another file as though it were part of **httpd.conf**.

.htaccess Local directives can appear in **.htaccess** files (above). A **.htaccess** file can appear in any directory within the document root hierarchy; it affects files in the directory hierarchy rooted at the directory the **.htaccess** file appears in.

Pathnames When you specify an absolute pathname in a configuration directive, the directive uses that pathname without modifying it. When you specify a relative pathname, such as a simple filename or the name of a directory, Apache prepends to the name the value specified by the **ServerRoot** (page 865) directive (**/etc/httpd** by default).

# ## DIRECTIVES I: DIRECTIVES YOU MAY WANT TO MODIFY AS YOU GET STARTED

When it starts, Apache reads the **/etc/httpd/conf/httpd.conf** configuration file (by default) for instructions governing every aspect of how Apache runs and delivers content. The **httpd.conf** file shipped by Fedora/RHEL is almost 1,000 lines long. This section details some lines you may want to change as you are getting started with Apache. You can use each of the following directives in **httpd.conf**; the Context line in each explanation shows which other files the directives can appear in. Context is explained on page 854. The section titled “Directives II: Advanced Directives” on page 858 describes more directives.