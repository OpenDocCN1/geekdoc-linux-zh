# flastmod  The flastmod command prints the last modification date of the specified file. Here is the syntax:

```
flastmod [ file = "path" ] [ virtual="URL"]
```

The output is subject to the timefmt format specification. For example:

```
<!-#flastmod file="free_software.zip">
```

```
<!-#flastmod virtual="/download/free_software.zip">
```

If you are unclear about the syntax difference, see the previous section regarding the fsize command as an example. To control how the modification date is printed, see the earlier description of the config command.

# include  The include directive inserts the text of a document into the SSI document being processed. Here is the syntax:

```
include [ file = "path" ] [ virtual="URL"]
```

See the previous description of the fsize command for an explanation of the difference between file and virtual mode.

Any included file is subject to the usual access control. If the directory containing the parsed file has the option IncludesNOEXEC set, and including the document would cause a program to be executed, then it is not included. This prevents the execution of CGI scripts. Otherwise, CGI scripts are invoked as they normally are, using the complete URL given in the command, including any query string. For example,

```
<!-#include file="copyrights.html" -->
```

includes the copyrights.html file in the current document. Recursive inclusions are detected, and an error message is generated after the first pass.

# printenv  The printenv command prints a listing of all existing variables and their values. Here is the syntax:

```
printenv
```

For example, the following prints all the Include and CGI environment variables available:

```
<!-#printenv -->
```