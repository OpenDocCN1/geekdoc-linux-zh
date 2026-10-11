# Appendix

# A

# Perl Built-ins, Pragmas, Modules, and the Debugger

# A.1 Perl Functions

The following is a complete list of Perl functions and a short description of what they do. Note: The text in parentheses is a reference to the like-named UNIX system call found in Section 2 of the UNIX manual pages. The like-named UNIX library functions are found in Section 3 of the UNIX manual pages.

Table A.1 Perl Functions

| Function | Description |
| :--- | :--- |
| abs | abs VALUE |
| | Returns the absolute value of its argument ($. is the default). Ignores signs. |
| accept | accept(NEWSOCKET, GENERICSOCKET) |
| | Accepts a socket connection from clients waiting for a connection. GENERICSOCKET, a filehandle, has been previously opened by the socket function, is bound to an address, and is listening for a connection. NEWSOCKET is a filehandle with the same properties as GENERICSOCKET. The accept function attaches GENERICSOCKET to the newly made connection. See accept(2). |
| alarm | alarm(SECONDS) |
| | alarm SECONDS Sends a SIGALARM signal to the process after a number of SECONDS. See alarm(3). |
| atan2 | atan2(X,Y) |
| | Returns the arctangent of XY in the range <pi>.