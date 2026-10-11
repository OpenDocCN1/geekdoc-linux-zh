
## Table A.1 Perl Functions (continued)

| Function    | Description                                                                                                                        |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------|
| system      | `system(LIST)`<br>`system LIST`                                                                                                 <br><br>Executes a shell command from a Perl script and returns. Like the `exec` function, except it `forks` first, and the script waits until the command has been executed. Control then returns to the script. The return value is the exit status of the program and can be obtained by dividing by 256 or right-shifting the lower 8 bits.<br>See `system`(3).                                              |

| Function    | Description                                                                                                                        |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------|
| syswrite    | `syswrite(FILEHANDLE, SCALAR, LENGTH, OFFSET)`<br>`syswrite(FILEHANDLE, SCALAR, LENGTH)`<br>`syswrite(FILEHANDLE, SCALAR)`                                                    <br><br>Returns the number of bytes written to `FILEHANDLE`. Writes `LENGTH` bytes from variable `SCALAR` to `FILEHANDLE`, starting at position `OFFSET`, if `OFFSET` is specified. Uses the `write` system call.<br>See `write`(2).                                                  |

| Function    | Description                                                                                                                        |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------|
| tell        | `tell(FILEHANDLE)`<br>`tell FILEHANDLE`                                                                                               <br><br>Returns the current file position, in bytes (starting at byte 0), for `FILEHANDLE`. Normally the returned value is given to the `seek` function in order to return to some position within the file.<br>See `lseek`(2).                                                    |

| Function    | Description                                                                                                                        |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------|
| telldir     | `telldir(DIRHANDLE)`<br>`telldir DIRHANDLE`                                                                                       <br><br>Returns the current position of the `readdir` function for the directory structure. `DIRHANDLE`.<br>See `directory`(3).                                                    |

| Function | Description |
| :--- | :--- |
| tie | `tie`(*VARIABLE, CLASSNAME, LIST*) |
|  | Binds a `VARIABLE` to a package (`CLASSNAME`) that will use methods to provide the implementation for the variable. `LIST` consists of any additional arguments to be passed to the new method when constructing the object. Most commonly used with associative arrays to bind them to databases. |
|  | The methods have predefined names to be placed within a package. The predefined methods will be called automatically when the tied variables are fetched, stored, destroyed, etc. |
|  | The package implementing an associative array provides the following methods: |
|  | `TIEHASH` $classname, *LIST* |
|  | `DESTROY` Self |
|  | `FETCH` Self, *$key* |
|  | `STORE` Self, *$key* |
|  | `DELETE` Self, *$key* |
|  | `EXISTS` Self, *$key* |
|  | `FIRSTKEY` Self |
|  | `NEXTKEY` Self, *$lastkey* |
|  | Methods provided for an array are: |
|  | `TIEARRAY` $classname, *LIST* |
|  | `DESTROY` Self |
|  | `FETCH` Self, *$subscript* |
|  | `STORE` Self, *$subscript*, *$value* |
|  | Methods provided for a scalar are: |
|  | `TIESCALAR` $classname, *LIST* |
|  | `DESTROY` Self |
|  | `FETCH` Self |
|  | `STORE` Self, *$value* |
|  | Example: |
|  | ```perl
|  | $object = tie $hash, Myhashclass
|  | while ($key, $value)=each ($hash){
|  |     print "$key, $value\n" # invokes the FETCH method
|  | }
|  | $object = tie $array, Myarrayclass
|  | $array[0]=5 # invokes the STORE method
|  | $object = tie $scalar, Myscalarclass
|  | until $scalar # invokes the DESTROY method
|  | ``` |
| tied | `tied` *VARIABLE* |
|  | Returns a reference to the object that was previously bound with the `tie` function or undefined if `VARIABLE` is not tied to a package. |

| Function | Description |
| :------- | :---------- |
| time | <i>time</i> |
| | Returns a 4-element array of non-leap-year seconds since January 1, 1970, UTC. Used with <i>gmtime</i> and <i>localtime</i> functions. |
| | See <i>ctime</i>(3). |
| times | <i>times</i> |
| | Returns a 4-element array giving the user and system CPU times, in seconds, for the process and its children. |
| | See <i>times</i>(3). |
| tr | <i>tr</i>(SEARCHPATTERN/REPLACEMENT/[c|d|d]) |
| | <i>y</i>(SEARCHPATTERN/REPLACEMENT/[c|d|d]) |
| | Translates characters in SEARCHPATTERN to corresponding character in REPLACEMENT. Similar to UNIX <i>tr</i> command. |
| truncate | <i>truncate</i>(FILEHANDLE, LENGTH) |
| | <i>truncate</i>(EXPR, LENGTH) |
| | Truncate FILEHANDLE or EXPR to a specified LENGTH. |
| | See <i>truncate</i>(2). |
| uc | <i>uc</i> EXPR |
| | Returns EXPR (or `$_` if no EXPR) in uppercase letters. Same as /\uE escape sequences. |
| ucfirst | <i>ucfirst</i> EXPR |
| | Returns the first character of EXPR (or `$_` if no EXPR) in uppercase. Same as /\u escape sequence. |
| umask | <i>umask</i>(EXPR) |
| | <i>umask</i> EXPR |
| | <i>umask</i> |
| | Sets the <i>umask</i> (file creation mask) for the process and returns the old <i>umask</i>. With EXPR omitted, returns the current <i>umask</i> value. |
| | See <i>umask</i>(2). |
| undef | <i>undef</i>(EXPR) |
| | <i>undef</i> EXPR |
| | <i>undef</i> |
| | Undefines EXPR, an lvalue. Used on scalars, arrays, hashes, or subroutine names (\&subroutine) to recover any storage associated with it. Always returns the undefined value. Can be used by itself when returning from a subroutine to determine if an error was made. |

| Function | Description |
| :------- | :---------- |
| `unlink` | `unlink(LIST)`<br>`unlink LIST`<br>`unlink`<br>Removes a LIST of files. Returns the number of files deleted. Without an argument, unlinks the value stored in `$_`. See `unlink`(2). |
| `unpack` | `unpack(TEMPLATE, EXPR)`<br>Unpacks a string representing a structure and expands it to an array value, returning the array value, using TEMPLATE to get the order and type of values. Reverse of `pack`. |
| `unshift` | `unshift(LIST)`<br>`unshift`<br>Prepends LIST to the beginning of an array. Returns the number of elements in the new array. |
| `untie` | `untie VARIABLE`<br>Breaks the binding (unties) between a variable and the package it is tied to. Opposite of `tie`. |
| `use` | `use MODULE VERSION LIST`<br>`use MODULE LIST`<br>`use MODULE`<br>`use MODULE()`<br>`use pragma`<br>A compiler directive that imports subroutines and variables from MODULE into the current package. VERSION is the current version number of Perl. LIST consists of specific names of the variables and subroutines the current package will import. Use empty parameters if you don't want to import anything into your namespace. The -m and -M flags can be used at the command line instead of use. Pragmas are a special kind of module that can affect the behavior for a block of statements at compile time. Three common pragmas are `integer`, `subs`, and `strict`. |
| `utime` | `utime(LIST)`<br>`utime LIST`<br>Changes the access and modification times on a list of files. The first two elements of LIST are the numerical access and modification times. |
| `values` | `values(%ASSOC_ARRAY)`<br>`values ASSOC_ARRAY`<br>Returns an array consisting of all the values in an associative array, ASSOC_ARRAY, in random order. |
