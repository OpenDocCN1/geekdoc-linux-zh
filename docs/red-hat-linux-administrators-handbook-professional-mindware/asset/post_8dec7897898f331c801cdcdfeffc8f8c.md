
...information for each request to tell the Web browser what type of content is being sent as the response. Therefore, you need to tell Apache that when responding to an .shtml file request, it should tell the browser, by setting the content type, that the information being sent is still an HTML document. This way, the Web browser will render the content onscreen as usual.

The MIME type for HTML content is `text/html`. The following line shows how to instruct Apache to generate a `text/html` content type header when transmitting the output of an .shtml page:

```
AddType text/html .shtml
```

For backward-compatibility, documents with the MIME type `text/x-server-parsed-html` or `text/x-server-parsed-html3` will also be parsed (and the resulting output is given the MIME type `text/html`).

## Enable SSI parsing of a directory

Both Apache and Web browsers know how to handle the new .shtml files; however, Apache is still not ready to parse the .shtml pages.

Using the `Options` directive, you need to tell Apache that you want to enable Includes support. First, however, you need to determine where to put this `Options` directive.

If you want to enable SSI support in the entire (primary) Web site, add the following directive in one of the global configuration files (such as `access.conf`):

```
Options +Includes
```

If you want to enable SSI support for a virtual Web site, put the preceding directive inside the appropriate `<VirtualHost ...>` container. Or, if you want to be able to control this option from directory to directory, put this directive inside a `<Directory ...>` container or in the per-directory access control file (`.htaccess`).

If you use a per-directory access control file (`.htaccess`) to enable SSI support, make sure the `AllowOverride` directive for the site owning that directory allows the Includes option to be overridden. For example, if the `AllowOverride` is set to `None` for a site, no SSI parsing will occur.

If you do not use the `+` sign in the `Options` line in the preceding example, all the options except Includes will be disabled.

## Using SSI commands

SSI commands are embedded in HTML pages in the form of comments. The base command structure looks like this:

```
<!--#command argument1=value argument2=value argument3=value -->
```

The value is often enclosed in double quotes; many commands allow only a single attribute-value pair. The comment terminator (`-->`) should be preceded by whitespace to ensure that it isn't considered part of the SSI command.

Next, the config, echo, exec, fsize, lastmod, include, printenv, and set SSI commands are examined.

### config

The `config` command enables you to configure error messages and output formats. Here is the syntax:

```
config [errmsg="error message"] [sizefmt=["bytes" | "abbrev"]] [timefmt=format_string]
```

For example:

```
<!--#config errmsg="This is a custom SSI error message." -->
<!--#config errmsg_type="This is a custom error message." -->
```

The first command is a valid `config errmsg` command that sets the error message to the string "This is a custom SSI error message." The second command is an invalid SSI command that causes a parse error; the error message "This is a custom SSI error message" is displayed as a result. The message appears where the invalid command is found. It is possible to enter HTML tags or even insert client-side script in the string of the error message.

To configure the output format for the file size, use the `config sizefmt=["bytes" | "abbrev"]` command. Acceptable format specifiers are "bytes" or "abbrev". For example,

```
<!--#config sizefmt="bytes" -->
```

shows file sizes in bytes. To show files in kilobytes or megabytes, use the following:

```
<!--#config sizefmt="abbrev" -->
```

To configure the display format for time, use the `config timefmt=format_string` command. The commonly used value of the format string may consist of the identifiers shown in Table 12-2.

### Table 12-2 The format specifiers for timefmt

| Identifier | Description |
|---|---|
| `%a` | The abbreviated weekday name according to the current locale |
| `%A` | The full weekday name according to the current locale |
| `%b` | The abbreviated month name according to the current locale |
| `%B` | The full month name according to the current locale |
| `%c` | The preferred date and time representation for the current locale |
| `%d` | The day of the month as a decimal number (range 01 to 31) |
| `%H` | The hour as a decimal number using a 24-hour clock (range 00 to 23) |
| `%I` | The hour as a decimal number using a 12-hour clock (range 01 to 12) |
| `%j` | The day of the year as a decimal number (range 001 to 365) |
| `%m` | The month as a decimal number (range 01 to 12) |
| `%M` | The minute as a decimal number |
| `%p` | Either a.m. or p.m., according to the given time value or locale |
| `%s` | The second as a decimal number |
| `%w` | The day of the week as a decimal, Sunday being 0 |
| `%x` | The preferred date representation for the current locale without the time |
| `%X` | The preferred time representation for the current locale without the date |
| `%y` | The year as a decimal number without a century (range 00 to 99) |
| `%Y` | The year as a decimal number including the century |
| `%z` | The time zone name or abbreviation |
| `%%` | A literal `%` character |

For example, the following shows the time in the format 05/20/2000:

```
<!--#config timefmt="%m/%d/%Y" -->
```

### echo

The `echo` command prints one of the Include variables or any of the CGI environment variables. Here is the syntax:

```
echo var="variable name"
```

If the value of the variable is not available, it prints “(none)” as the value. Any dates printed are subject to the currently configured `timefmt`. For example,

```
<!--#config timefmt="%m/%d/%Y" -->
<!--#echo var="DATE_LOCAL" -->
```

prints a date, such as 05/20/2000, because of the specified `timefmt` string.

### exec

The `exec` command enables you to execute an external program, which can be a CGI program or any other type of executable, such as shell scripts or native-binary files. Here is the syntax:

```
exec [cgi=path/to/cgi/program] [cmd=path/to/other/program -]
```

If you use the `IncludesNOEXEC` value for the `Options` directive, the `exec` command is disabled. The `exec cgi` command runs the named program as a CGI script, and the `exec cmd` command runs the named program using the `sh` (`/bin/sh`) shell as an external program.

### fsize

The `fsize` command prints the size of the specified file. Here is the syntax:

```
fsize [ file="path" ] [-] [ virtual="URL"]
```

When the first syntax (`file="path"`) is used, the path is assumed to be relative to the directory containing the current SSI document being parsed. You can’t use `../` in the path, nor can you use absolute paths. You can’t access a CGI script in this fashion. You can, however, access another parsed document. For example:

```
<!--#fsize file="download.zip" -->
```

If the second syntax (`virtual="URL"`) is used, the virtual path is assumed to be a ($-encoded) URL path. If the path does not begin with a slash (`/`), then it is taken to be relative to the current document. You must access a normal file this way, but you cannot access a CGI script in this fashion.

### flastmod

The `flastmod` command prints the last modification date of the specified file. Here is the syntax:

```
flastmod [ file = "path" ] [ virtual="URL"]
```

The output is subject to the `timefmt` format specification. For example:

```
<!--#flastmod file="free_software.zip" -->
<!--#flastmod virtual="/download/free_software.zip" -->
```

If you are unclear about the syntax difference, see the previous section regarding the `fsize` command as an example. To control how the modification date is printed, see the earlier description of the `config` command.

### include

The `include` directive inserts the text of a document into the SSI document being processed. Here is the syntax:

```
include [ file = "path" ] [ virtual="URL"]
```

See the previous description of the `fsize` command for an explanation of the difference between `file` and `virtual` mode.

Any included file is subject to the usual access control. If the directory containing the parsed file has the option `IncludesNOEXEC` set, and including the document would cause a program to be executed, then it is not included. This prevents the execution of CGI scripts. Otherwise, CGI scripts are invoked as they normally are, using the complete URL given in the command, including any query string. For example,

```
<!--#include file="copyrights.html" -->
```

includes the `copyrights.html` file in the current document. Recursive inclusions are detected, and an error message is generated after the first pass.

### printenv

The `printenv` command prints a listing of all existing variables and their values. Here is the syntax:

```
printenv
```

For example, the following prints all the Include and CGI environment variables available:

```
<!--#printenv -->
```
