# Table A.1 Perl Functions (continued)

| Function | Description |
| --- | --- |
| *dump* | *dump LABEL* |
| | Causes an immediate binary image core dump. The *undump* command, used for undumping a core file, is not part of the Perl 5.6.0 distribution. |
| *each* | *each*(%ASSOC_ARRAY) |
| | *each* %ASSOC_ARRAY |
| | Returns a two-element array, the key and value for the next value of an associative array, in random order. |
| *eof* | *eof*(*FILEHANDLE*) |
| | *eof*() |
| | *eof* |
| | Returns 1 if the next read on *FILEHANDLE* indicates the end of file. If *FILEHANDLE* is omitted, it returns the end of file for the last file read. |
| *eval* | *eval*(EXPR) |
| | *eval* EXPR |
| | Evaluates EXPR as a Perl program in the context of the current Perl script. Often used for trapping otherwise fatal errors. Syntax errors or runtime errors or those coming from the *die* function are returned to the $@ variable. The $@ variable is set to *NULL* if there are no errors. The value returned is the value of the last expression evaluated. |
| *exec* | *exec*(LIST) |
| | *exec* LIST |
| | Executes a system command LIST in context of the current program. Never returns. If LIST is scalar, checks for *shell* metacharacters and *passes* them to *bin/sh*. Otherwise, arguments are passed to the C function call *execvp*. Does not flush output buffer. |
| *exists* | *exists* EXPR |
| | Returns *TRUE* if a specified key from an associative array exists, even if its corresponding value is *undefined*. |
| *exit* | *exit*(INTEGER) |
| | *exit* INTEGER |
| | Exits with script with status value of INTEGER. If INTEGER is omitted, exits with 0, meaning the program exits with successful status. A nonzero status implies that something went wrong in the program. |
| *exp* | *exp*(EXPR) |
| | *exp* EXPR |
| | The exponential function. Returns *e* to the power of EXPR. |