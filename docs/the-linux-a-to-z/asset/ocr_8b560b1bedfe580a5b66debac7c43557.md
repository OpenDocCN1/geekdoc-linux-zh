```
e1 -o e2 -a e3
```

will evaluate as:

```
( e1 -o e2 ) -a e3
```

unless brackets are added explicitly to change this, as in:

```
e1 -o ( e2 -a e3 )
```

A logical not operator is also available, so that:

! e1 is true when e1 is false, and vice versa

The following table details some of the expressions that are available with find, along with the type of each expression and the value it returns:

| Expression | Description |
|---|---|
| -mount | An option expression which prevents find from searching outside the boundaries of the current filesystem. The return value is always true. |
| -group grp | A condition expression which checks the current file to see if it has a group ID or group name that matches grp. Return value is true if file's group ID or group name matches grp or false otherwise. |
| -name pattern | A condition expression which looks for a file name that matches pattern. The pattern can be given as a regular expression which may need quoting from the shell. Returns true if the current file name matches pattern or false otherwise. |
| -type t | A condition expression which checks to see if the current file is of type t, where t can be d for a directory, f for an ordinary file, l for a symbolic link, etc. Returns true if the current file is of type t or false otherwise. |
| -user usr | A condition expression which checks the current file to see if it has owner ID or owner name that matches usr. Return value is true if file's owner ID or owner name matches usr or false otherwise. |
| -exec cmd ; | An action expression which executes the command cmd. If you need to pass the current file name to cmd this is done with the notation {}. The semicolon (;) is used to mark the end of cmd and separate it from any more option expressions that may follow. The return value is true if the cmd executes successfully without error or false otherwise. |
| -print | An action expression which just prints the current file name to the standard output device. Always returns true. |