
## A.1 Perl Functions

### Table A.1 Perl Functions (continued)

| Function | Description |
| :--- | :--- |
| **oct** | `oct(EXPR)`<br>`oct EXPR`<br><br>Returns the decimal value of *EXPR*, an octal string. If *EXPR* contains a leading 0x, *EXPR* is interpreted as hex. With no *EXPR*, $_ is converted. |
| **open** | `open(FILEHANDLE, EXPR)`<br>`open(FILEHANDLE)`<br>`open FILEHANDLE`<br><br>Opens a real file, *EXPR*, and attaches it to *FILEHANDLE*. Without *EXPR*, a scalar with the same name as *FILEHANDLE* must have been assigned that filename.<br><br>- `"FILEHANDLE"`: read<br>- `">>FILEHANDLE"`: write<br>- `">>>FILEHANDLE"`: read/write<br>- `">>>FILEHANDLE"`: append<br>- `"\|UNIX Command"`: pipe out<br>- `"*UNIX Command \|"`: pipe in |

| Function | Description |
| :--- | :--- |
| **pack** | `$packed=pack(TEMPLATE, LIST)`<br><br>Packs a list of values into a binary structure and returns the structure. `TEMPLATE` is a quoted string containing the number and type of value. `TEMPLATE` is:<br>- **a** An ASCII string, null padded<br>- **A** An ASCII string, space padded<br>- **b** A bit string, low-to-high order<br>- **B** A bit string, high-to-low order<br>- **h** A hexadecimal string, low nybble first<br>- **H** A hexadecimal string, high nybble first<br>- **c** A signed char value<br>- **C** An unsigned char value<br>- **s** A signed short value<br>- **S** An unsigned short value<br>- **i** A signed integer value<br>- **I** An unsigned integer value<br>- **l** A signed long value<br>- **L** An unsigned long value<br>- **n** A short in 'network' order<br>- **N** A long in 'network' order<br>- **f** A single-precision float in native format<br>- **d** A double-precision float in native format<br>- **p** A pointer to a string<br>- **x** A null byte<br>- **X** Back up a byte<br>- **@** Null-fill to absolute precision<br>- **u** A uencoded string |
| **package** | `package NAMESPACE`<br><br>A package declaration creates a separate namespace (symbol table) for `NAMESPACE`, the Perl way of creating a class. The `NAMESPACE` belongs to the rest of the innermost enclosing block, subroutine, `eval`, or file. If the package declaration is at the same level, the new one overrides the old one. |
| **pipe** | `pipe(READHANDLE, WRITEHANDLE)`<br><br>Opens a pipe for reading and writing, normally after a *fork*. See `pipe(2)`. |
| **pop** | `pop ARRAY`<br>`pop(ARRAY)`<br><br>Pops and returns the last element of the array. The array will have one less element. |

| Function | Description |
| :--- | :--- |
| **pos** | `pos(SCALAR)`<br>`pos SCALAR`<br><br>Returns the offset of the character after the last matched search in SCALAR<br>left off; i.e., the position where the next search will start. Offsets start at 0.<br>If the *$scalar* is a signed `\hello` and the search is *$scalar* = *m*/*elig*, the<br>pos function would return the position of the character after the first *1*.<br>position 3. |
| **print** | `print(FILEHANDLE LIST)`<br>`print(LIST)`<br>`print FILEHANDLE LIST`<br>`print LIST`<br>`print`<br><br>Prints a string or a comma-separated list of strings to FILEHANDLE or to<br>the currently selected FILEHANDLE or to STDOUT, the default. Returns 1 if<br>successful, 0 if not. |
| **printf** | `printf(FILEHANDLE FORMAT, LIST)`<br>`printf(FORMAT, LIST)`<br><br>Prints a formatted string to FILEHANDLE or, if FILEHANDLE is omitted, to<br>the currently selected output filehandle. STDOUT is the default. Similar to<br>Cs printf, except `*` is not supported.<br>See printf(3). |
| **prototype** | `prototype FUNCTION`<br><br>Returns the prototype of a function as a string, where FUNCTION is the<br>name of the function. Returns *undef* if there is no prototype. |
| **push** | `push(ARRAY, LIST)`<br><br>Pushes the values in LIST onto the end of the ARRAY. The array will be<br>increased. Returns the new length of ARRAY. |
| **q, qq, qw, qx** | `q/STRING/`<br>`qq/STRING/`<br>`qw/LIST/`<br>`qx/COMMAND/`<br><br>An alternative form of quoting. The *q* construct treats STRING as if enclosed<br>in single quotes. The *qq* construct treats STRING as if enclosed in double<br>quotes. The *qw* construct treats each element of LIST as if enclosed in single<br>quotes, and the *qx* treats COMMAND as if in backquotes. |
| **quotemeta** | `quotemeta EXPR`<br><br>Returns the scalar value of EXPR with all regular expression metacharacters<br>backslashed. |

| Function | Description |
| :--- | :--- |
| **rand** | `rand(EXPR)`<br>`rand EXPR`<br><br>`rand`<br><br>Returns a random fractional number (scalar) between 0 and EXPR, where EXPR is a positive number. Without rand generates the same sequence of numbers. If EXPR is omitted, returns a value between 0 and 1.<br>See rand(3). |
| **read** | `read(FILEHANDLE, SCALAR, LENGTH, OFFSET)`<br>`read(FILEHANDLE, SCALAR, LENGTH)`<br><br>Reads LENGTH number of bytes from FILEHANDLE, starting at position OFFSET, into SCALAR and returns the number of bytes read, or 0 if EOF (Similar to fread system call.)<br>See fread(3). |
| **readdir** | `readdir(DIRHANDLE)`<br>`readdir DIRHANDLE`<br><br>Reads the next entry of the directory structure, DIRHANDLE, opened by opendir. See directory(3). |
| **readline** | `readline FILEHANDLE`<br><br>Reads and returns a line from selected FILEHANDLE; e.g., $line = readline(STDIN). |
| **readlink** | `readlink(EXPR)`<br>`readlink EXPR`<br><br>Returns the value of a symbolic link. EXPR is the pathname of the symbolic link, and if omitted, $_ is used. See readlink(2). |
| **readpipe** | `readpipe scalar EXPR`<br>`readpipe LIST(proposed)`<br><br>An internal function that implements the qq// quote construct or backquotes for command substitution; e.g., to print the output of the UNIX ls command, type print readpipe( ). |
| **recv** | `recv(SOCKET, SCALAR, LEN, FLAGS)`<br><br>Receives a message of LEN bytes on a socket into SCALAR variable. Returns the address of the sender.<br>See recv(2). |
| **redo** | `redo LABEL`<br>`redo`<br><br>Restarts a loop block without reevaluating the condition. If there is a continue block, it is not executed. Without LABEL, restarts at the innermost enclosing loop. |

| Function | Description |
| :--- | :--- |
| **ref** | `ref EXPR`<br><br>Returns a scalar TRUE value, the data type of EXPR, if EXPR is a reference, else the NULL string. The returned value depends on what is being referenced, a REF, SCALAR, ARRAY, HASH, CODE, or GLOB. If EXPR is an object that has been blessed into a package, the return value is the package (class) name. |
| **rename** | `rename(OLDNAME, NEWNAME)`<br><br>Renames a file OLDNAME to NEWNAME. Does not work across filesystem boundaries. If NEWNAME already exists, it is destroyed.<br>See rename(2). |
| **require** | `require(EXPR)`<br>`require EXPR`<br>`require`<br><br>Includes file EXPR from the Perl library by searching the @INC array for the specified file. Also checks that the library has not already been included. $_ is used if EXPR is omitted. |
| **reset** | `reset(EXPR)`<br>`reset EXPR`<br>`reset`<br><br>Clears variables and arrays or, if EXPR is omitted, resets ?? searches. |
| **return** | `return LIST`<br><br>Returns a value from a subroutine. Cannot be used outside of a subroutine. |
| **reverse** | `reverse(LIST)`<br><br>Reverses the order of LIST and returns an array. |
| **rewinddir** | `rewinddir(DIRHANDLE)`<br>`rewinddir DIRHANDLE`<br><br>Rewinds the position in DIRHANDLE to the beginning of the directory structure.<br>See directory(3). |
| **rindex** | `rindex(STRING, SUBSTR, OFFSET)`<br>`rindex(STRING, SUBSTR)`<br><br>Returns the last position of SUBSTR in STRING starting at OFFSET, if OFFSET is specified like index but returns the last position of the substring rather than the first. |
| **rmdir** | `rmdir(FILENAME)`<br>`rmdir FILENAME`<br><br>Removes a directory, FILENAME, if empty. |

| Function | Description |
| :--- | :--- |
| **s** | `s/SEARCH_PATTERN/REPLACEMENT/[g][l][o][e]`<br><br>Searches for SEARCH_PATTERN and, if found, replaces the pattern with some text. Returns the number of substitutions made. The g option is global across a line. The i option turns off case sensitivity. The e option evaluates the replacement string as an expression; e.g., $/d+\$&+$/e |
| **scalar** | `scalar (EXPR)`<br><br>Forces EXPR to be evaluated in a scalar context. |
| **seek** | `seek(FILEHANDLE, POSITION, WHENCE)`<br><br>Positions a file pointer in a file, FILEHANDLE, from some position, relative to its position in the file WHENCE. If WHENCE is 0, starts at the beginning of the file; if WHENCE is 1, starts at the current position of the file; and if WHENCE is 2, starts at the end of the file. POSITION cannot be negative if WHENCE is 0. |
| **seekdir** | `seekdir(DIRHANDLE, POSITION)`<br><br>Sets the POSITION for the readdir function on the directory structure associated with DIRHANDLE.<br>See directory(3). |
| **select** | `select(FILEHANDLE)`<br>`select`<br><br>Returns the currently selected filehandle if FILEHANDLE is omitted. With FILEHANDLE, sets the current default filehandle for write and print.<br>See Formatting. |
| **select** | `select(RBITS, WBITS, EBITS, TIMEOUT)`<br><br>Examines the I/O file descriptors to see if descriptors are ready for reading or writing or have exceptional conditions pending. Bitmasks are specified, and TIMEOUT is in seconds.<br>See select(2). |
| **semctl** | `semctl(ID, SEMNUM, CMD, ARG)`<br><br>Calls the semctl system call, allowing control operations on semaphores. Has weird return codes. Requires library files ipc.ph and sem.ph.<br>See System V IPC.<br>See also semctl(2). |
| **semget** | `semget(KEY, NSEMS, SIZE, FLAGS)`<br><br>Returns the semaphore ID associated with KEY, or undefined if an error. Requires library files ipc.ph and sem.ph.<br>See System V IPC.<br>See also semget(2). |
