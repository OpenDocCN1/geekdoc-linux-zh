# include

The `include` directive inserts the text of a document into the SSI document being processed. The syntax depends on the path to the directory:

+   - **Syntax 1:** `include file="path"`
+   - **Syntax 2:** `include virtual="URL"`

See the `fsize` command a couple sections back for the difference between file and virtual mode.

Any included file is subject to the usual access control. If the directory containing the parsed file has the `Option IncludesNOEXEC` set, and including the document would cause a program to be executed, then it is not included. This prevents the execution of CGI scripts. Otherwise, CGI scripts are invoked as they normally are, using the complete URL given in the command, including any query string. For example:

```
<!--#include file="copyrights.html" -->
```

includes the `copyrights.html` file in the current document. This command is useful for adding repeatable HTML code in files. Many sites use a standard menu bar on each page; if this menu bar is put in an HTML file called `menu.html`, it can be called from all SSI pages using a similar `include` file call, as in the preceding example. In the future, when changes need to be made to the menu, the site administrator only needs to update the `menu.html` page. This will save a lot of work if there are many files in the site.

Recursive inclusions are detected and an error message is generated after the first pass. For example, if `a.shtml` has an SSI call such as:

```
<!--#include file="b.shtml" -->
```

and `b.shtml` has a call such as:

```
<!--#include file="a.shtml" -->
```

then Apache logs and displays an error stating that a recursive include has been detected.

# printenv

The `printenv` command prints a listing of all existing variables and their values. The syntax is:

```
printenv
```