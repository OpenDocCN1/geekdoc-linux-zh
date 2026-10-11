```
LogFormat "%h %l %u %t "%r" %s %b"
TransferLog private/log
CustomLog private/log "%h %l %u %t "%r" %s %b"
```

The ``LogFormat`` directive changes the default format for logging. Table 16-16 shows the possible options. The ``TransferLog`` directive outputs the log to a new file, using the default format or the one specified for ``LogFormat``. ``CustomLog`` combines the previous two directives and sets up a new log file and format.

Table 16-16 LogFormat Arguments
|Argument|Function|
| %b|Bytes sent, not counting header information|
| %f|Filename|
| %{{VAR}}e|The value of variable `VAR`. For example, this can give you information on the client by using the `Referer` and `User-Agent` variables.|
| %h|Remote hostname|
| %{{foobar}}i|The contents of `foobar:` header line(s) in the request sent to the server|
| %l|Remote `logname` from `identd`|
| %{{foobar}}n|The value of note `foobar` from another module|
| %{{foobar}}o|The contents of `foobar:` header line(s) in the reply|
| %p|The port that the request was served to|
| %P|The process ID of the child process that handled the request|
| %r|The first line of the request|
| %s|Status|
| %t|The time of the request|
| %{{format}}t|The time given in the specified format|
| %T|The number of seconds taken to handle the request|
| %u|Remote user, taken from `ident`|
| %U|The URL of the path requested|
| %v|The name of the server that handled the request, used for virtual hosts|