# Table A.1 Perl Functions (continued)

| Function | Description |
| :--- | :--- |
| `vec` | `vec(EXPR, OFFSET, BITS)`
Treats a string, EXPR, as a vector of unsigned integers. Returns the value of the element specified. `OFFSET` is the number of elements to skip over in order to find the one wanted, and `BITS` is the number of bits per element in the vector. `BITS` must be one of a power of 2 from 1 to 32; e.g., 1, 2, 4, 8, 16, or 32. |
| `wait` | `wait`
Waits for the child process to terminate. Returns the `pid` of the deceased process and -1 if there are no child processes. The status value is returned in the $! variable.
See wait(2). |
| `waitpid` | `waitpid(FLAGSPID, FLAGS)`
Waits for a child process to terminate and returns true when the process dies or -1 if there are no child processes or if `FLAGS` specify nonblocking and the process hasn't died. $? gets the status of the dead process. Requires `sys/wait.ph`.
See wait(2). |
| `wantarray` | `wantarray`
Returns true if the context of the currently running subroutine wants an array value, i.e., the returned value from the subroutine will be assigned to an array. Returns false if looking for a scalar.
Example: `return wantarray ? 0 : undef` |
| `warn` | `warn(LIST)`
`warn LIST`
Sends a message to STDERR, like the `die` function, but doesn't exit the program. |
| `write` | `write(FILEHANDLE)`
`write FILEHANDLE`
`write`
Writes a formatted record to `FILEHANDLE` or currently selected `FILEHANDLE` (see select); i.e., when called, invokes the format (picture line) for the `FILEHANDLE`, with no arguments. Goes either to STDOUT or to the `FILEHANDLE` currently selected by the select call. Has nothing to do with the write(2) system call.
See syswrite. |
| `y` | `y/SEARCHPATTERN/REPLACEMENT/[c][d][e]`
Translates characters in `SEARCHPATTERN` to corresponding characters in `REPLACEMENT`. Also known as `tr` and similar to UNIX `tr` command or `sed` y command. |