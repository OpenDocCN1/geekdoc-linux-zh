
# Table A.1 Perl Functions

| Function | Description |
| :------- | :---------- |
| getservbyport | `getservbyport(PORT_NUMBER, PROTOCOL)`<br>From `*/etc/services*` database, translates a port number to its corresponding port name as a scalar and returns as an array the service name, aliases, port where service resides, and protocol needed, from the `*/etc/services*` database.<br>In scalar context, returns only the service port number.<br>See `getservent(3)`. |
| getservent | `getservent`<br>`setservent(STAYOPEN)`<br>`endservent`<br>Iterates through the `*/etc/services*` database, returning the service name, aliases, port where service resides, and protocol needed. If `STAYOPEN` flag is nonzero, the database will not be closed during subsequent calls and `*endservent*` closes the file. In scalar context, returns only the service port name.<br>See `getservent(3)`. |
| getsockname | `getsockname(SOCKET)`<br>Returns the packed socket addr address of the local end of the `SOCKET` connection.<br>See `getsockname(2)`. |
| getsockopt | `getsockopt(SOCKET, LEVEL, OPTNAME)`<br>Returns the requested options, `OPTNAME`, associated with `SOCKET` at the specified protocol `LEVEL`.<br>See `getsockopt(2)`. |
| glob | `glob EXPR`<br>Performs filename expansion on `EXPR` as the `*shell*` does. Without `EXPR`, `$*` is used. Uses the internal `<>` operator. |
| gmtime | `gmtime(EXPR)`<br>`gmtime EXPR`<br>Converts the results of the `*time*` function to a 9-element array with the Greenwich Mean Time zone, including the second, minute, hour, day of the month, month, year, day of the week, day of the year, and 1 if daylight saving time is in effect.<br>See `ctime(3)` and `timegm()` in the Perl library module `Time::Local`. |
| goto | `goto LABEL`<br>`goto EXPR`<br>`goto &NAME`<br>Program branches to the `LABEL` and resumes execution. Cannot `goto` any construct that requires initialization, such as a subroutine or `*foreach*` loop. `GoGoto` never returns a value. The form `*goto* &NAME` substitutes the currently running subroutine with a call to `NAME` (used by the `AUTOLOAD` subroutine). |
| grep | `grep(EXPR, LIST)`<br>`grep BLOCK LIST`<br>Returns to a new array any element in `LIST` where `*EXPR*` matches that element. Returns a scalar, the number of matches. |
| hex | `hex(EXPR)`<br>`hex EXPR`<br>Returns the decimal value of `*EXPR*` interpreted as a hexadecimal string. Without `*EXPR*`, uses `$_`. |
| import | `import CLASSNAME LIST`<br>`import CLASSNAME`<br>Not a built-in function but a class method defined by modules that will export names to other modules through the `*use*` function. |
| index | `index(STR, SUBSTR, POSITION)`<br>`index(STR, SUBSTR)`<br>Returns the position of the first occurrence of `*SUBSTR*` in `*STR*`. `*POSITION*` specifies a starting position for the substring in the string starting with base 0. |
| int | `int(EXPR)`<br>`int EXPR`<br>Returns the integer portion of `*EXPR*`. Without `*EXPR*`, `$_` is used. |
| ioctl | `ioctl(FILEHANDLE, FUNCTION, SCALAR)`<br>Used to control I/O operations, mainly terminal I/O. Requires `*sysioctl.ph*`. `*FUNCTION*` is an I/O request. `*SCALAR*` will be read or written depending on the request.<br>See `*ioctl*(2)`. |
| join | `join(EXPR, LIST)`<br>Returns a single string by joining the separate strings of `*LIST*` into a single string where the field separator is specified by `*EXPR*`, a delimiter. |
| keys | `keys(%ASSOC_ARRAY)`<br>`keys %ASSOC_ARRAY`<br>Returns a normal array consisting of all the keys in the associative array. |
| kill | `kill(SIGNAL, PROCESS_LIST)`<br>`kill PROCESS_LIST`<br>Sends a `*SIGNAL*` to a list of processes. The `*SIGNAL*` can be either a number or a signal name (signal name must be quoted). (Negative `*SIGNAL*` number kills process group.)<br>See `*kill*(2)`. |
| last | `last LABEL`<br>The `last` command is comparable to C's `break` command. It exits the innermost loop or, if the loop is labeled `last LABEL`, exits that loop. |
| lc | `lc EXPR`<br>Returns `EXPR` in lowercase. Same as `\L \E` escape sequence. |
| lcfirst | `lcfirst EXPR`<br>Returns `EXPR` with the first character in lowercase. Same as `\U \E` sequence. |
| length | `length(EXPR)`<br>`length EXPR`<br>Returns the length in characters of scalar `EXPR` or, if `EXPR` is omitted, returns length of `$_`. Not used to find the size of an array or associative array. |
| link | `link(OLDFILE, NEWFILE)`<br>Creates a hard link. `NEWFILE` is another name for `OLDFILE`.<br>See `link(2)`. |
| listen | `listen(SOCKET, QUEUESIZE)`<br>Listens for connections on a `SOCKET` with a `QUEUESIZE` specifying the number of processes waiting for connections.<br>See `listen(2)`. |
| local | `local(LIST)`<br>Makes variables in `LIST` local for this block, subroutine, or `eval`. |
| localtime | `localtime(EXPR)`<br>`localtime EXPR`<br>Converts the time returned by the `time` function to a 9-element array for the local time zone. The array consists of:<br>- seconds<br>- minutes<br>- hours<br>- day of the month<br>- number of the month (0 is January)<br>- years since 1990<br>- day of the week (0 is Sunday)<br>- day of the year (0 is January 1)<br>- isdst (true if daylight savings is on)<br>See `ctime(3)`. |
| lock | `lock THING`<br>Places a lock on a variable, subroutine, or object referenced by `THING` until the lock goes out of scope. Used only with threads if they are enabled. |
| log | `log(EXPR)`<br>`log EXPR`<br>Returns the logarithm (base `e`) of `EXPR`. If `EXPR` is omitted, returns `log($_)`. |
| lstat | `lstat(FILEHANDLE)`<br>`lstat FILEHANDLE`<br>`lstat(EXPR)`<br>Returns a 14-element array consisting of file statistics on a symbolic link, rather than the file the symbolic link points to. The array consists of:<br>- device<br>- file inode number<br>- file mode<br>- number of hard links to the file<br>- user ID of owner<br>- group ID of owner<br>- raw device<br>- size of file<br>- file last access time<br>- file last modify time<br>- file last status change time<br>- preferred block size for filesystem I/O<br>- actual number of blocks allocated<br>See `stat(2)`. |
| m | `/*PATTERN*/`<br>`m/*PATTERN*/`<br>`m` is the match operator that interprets `PATTERN` as a regular expression and is used when alternative delimiters are needed, such as `mi/*PATTERN`. |
| map | `map(BLOCK, LIST)`<br>`map(EXPR, LIST)`<br>Evaluates `BLOCK` or `EXPR` for each element of `LIST` and returns the list value containing the results of the evaluation. The following example translates a list of numbers to characters: `@chars = map chr, @numbers` |
| mkdir | `mkdir(NAME, MODE)`<br>Creates a directory, `NAME`, with `MODE` permissions (octal).<br>See `mkdir(2)`. |
| msgctl | `msgctl(MSqid, CMD, FLAGS)`<br>Calls the `msgctl` system call, allowing control operations on a message queue. Has weird return codes. Requires library files `ipc.ph` and `msg.ph`.<br>See System V IPC.<br>See also `msgctl(2)`. |
| msgget | `msgget(KEY, FLAGS)`<br>Calls `msgget` system call. Returns the message queue ID number or, if undefined, an error.<br>See System V IPC.<br>See also `msgget(2)`. |
| msgrcv | `msgrcv(MSQID, VAR, MSG_SIZE, TYPE, FLAGS)`<br>Calls the `msgrcv` system call. Receives a message from the message queue, stores the message in `VAR`. `MSG_SIZE` is the maximum message size, and `TYPE` is the message type.<br>See System V IPC.<br>See also `msgrcv(2)`. |
| msgsnd | `msgsnd(ID, MSG, FLAGS)`<br>Calls the `msgsnd` system call. Sends the message `MSG` to the message queue. `MSG` must begin with the message type. The `pack` function is used to create the message.<br>See System V IPC.<br>See also `msgsnd(2)`. |
| my | `my TYPE EXPR : ATTRIBUTES`<br>`my EXPR : ATTRIBUTES`<br>`my TYPE EXPR`<br>`my EXPR`<br>Variables declared with the `my` function are made private; i.e., they exist only within the innermost enclosing block, subroutine, eval, or file. Only simple scalars, complete arrays, and hashes can be declared with `my`. `TYPE` and `ATTRIBUTES` optional and experimental at this time. |
| new | `new CLASSNAME LIST`<br>`new CLASSNAME`<br>Not a built-in function but a constructor method defined by the `CLASSNAME` module for creating `CLASSNAME`-type objects. Convention taken from C++. |
| next | `next LABEL`<br>Starts the next iteration of the innermost or loop labeled with `LABEL`. Like the C `continue` function. |
| no | `no MODULE LIST`<br>If a pragma or module has been imported with `use`, the `no` function says you don't want to use it anymore. |
| not | `not EXPR`<br>Logically negates the truth value of `EXPR`. |
