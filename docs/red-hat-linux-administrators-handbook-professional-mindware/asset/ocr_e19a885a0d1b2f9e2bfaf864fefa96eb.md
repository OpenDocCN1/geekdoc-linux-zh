LogFormat directive. If the format includes any spaces (which it will in almost all cases), it should be enclosed in double quotation marks.

Instead of an actual format string, you can use a format nickname defined with the LogFormat directive. (Nicknames are available only in Apache 1.3 or later.) Also, the *TransferLog* and *CustomLog* directives can be used multiple times in each server to cause each request to be logged to multiple files.

```
CookieLog filename
```

The CookieLog directive sets the filename for the logging of cookies. The filename is relative to the ServerRoot. This directive is included only for compatibility with *mod\_cookies* and is deprecated; therefore, use of this directive is not recommended. Use the user-tracking module's directive instead. The user-tracking module *mod\_usertrack* is discussed later in this chapter.

# ## Customizing server log files

Although CLF meets most log requirements, sometimes you'll want to be able to customize your logging data. For example, you may want to log the type of browsers that are accessing your sites, so that your Web design team can determine what type of browser-specific HTML to avoid or use. Or, perhaps you want to know which Web sites are sending (referring) visitors to your sites. All of this is accomplished quite easily in Apache. The default logging module, *mod\_log\_config*, supports custom logging.

Custom formats are set with the LogFormat and CustomLog directives of the module. The format argument to LogFormat and CustomLog is a string that can have both literal characters and special % format specifiers. When literal values are used in this string, they are copied into the log file for each request. The % specifiers, however, are replaced with corresponding values. The special % specifiers are described in Table 12-4.

### Table 12-4 % Specifiers for LogFormat

| Specifier | Description |
| :--- | :--- |
| %b | Bytes sent, excluding HTTP headers. |
| %f | The filename of the request. |
| %{*variable*}e | The contents of the environment variable *VARIABLE*. |