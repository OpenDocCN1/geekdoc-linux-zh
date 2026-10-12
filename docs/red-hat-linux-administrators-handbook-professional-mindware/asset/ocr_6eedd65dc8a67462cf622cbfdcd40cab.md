# Chapter 12: Web Service Using Apache

If the value of the variable is not available, it prints “(none)” as the value. Any dates printed are subject to the currently configured timefmt. For example,

```
<!--#config timefmt="%m/%d/%Y" -->
<!--#echo var="DATE_LOCAL" -->
```

prints a date, such as 05/20/2000, because of the specified timefmt string.

**exec** The exec command enables you to execute an external program, which can be a CGI program or any other type of executable, such as shell scripts or native-binary files. Here is the syntax:

```
exec [cgi=path/to/cgi/program] [cmd=path/to/other/program -]
```

If you use the IncludesNOEXEC value for the Options directive, the exec command is disabled. The exec cgi command runs the named program as a CGI script, and the exec cmd command runs the named program using the sh (/bin/sh) shell as an external program.

**fsize** The size command prints the size of the specified file. Here is the syntax:

```
fsize [ file="path" ] [-] [ virtual="URL"]
```

When the first syntax (file="path") is used, the path is assumed to be relative to the directory containing the current SSI document being parsed. You can’t use . . / in the path, nor can you use absolute paths. You can’t access a CGI script in this fashion. You can, however, access another parsed document. For example:

```
<!--#fsize file="download.zip" -->
```

If the second syntax (virtual="URL") is used, the virtual path is assumed to be a ($-encoded) URL path. If the path does not begin with a slash (/), then it is taken to be relative to the current document. You must access a normal file this way, but you cannot access a CGI script in this fashion.