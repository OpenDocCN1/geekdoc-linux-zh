# **config**

The config command enables you to configure error messages and output formats. Here is the syntax:

```
config [errmsg="error message"] [sizefmt="bytes" | "abbrev"] [timefmt=format string]
```

For example,

```
<!--#config errmsg="This is a custom SSI error message." -->
<!--#config errmsg_typo="This is a custom error message." -->
```

The first command is a valid config errmsg command that sets the error message to the string "This is a custom SSI error message." The second command is an invalid SSI command that causes a parse error; the error message "This is a custom SSI error message." is displayed as a result. The message appears where the invalid command is found. It is possible to enter HTML tags or even insert client-side script in the string of the error message.

To configure the output format for the file size, use the config sizefmt=["bytes" | "abbrev"] command. Acceptable format specifiers are "bytes" or "abbrev". For example,

```
<!-- config sizefmt="bytes" -->
```

shows file sizes in bytes. To show files in kilobytes or megabytes, use the following:

```
<!-- config sizefmt="abbrev" -->
```

To configure the display format for time, use the config timefmt=format string command. The commonly used value of the format string may consist of the following identifiers:

For example, the following shows the time in the format 05/20/1998:

```
<!--#config timefmt="%m/%d/%Y" -->
```

# **echo**

The echo command prints one of the Include variables or any of the CGI environment variables. Here is the syntax:

```
echo var="variable name"
```