# TESTS (CONT.)

**Use This Test**

**To Do This**

+   *   **-perm permissions**
+       *   Match files with the specified permissions (octal or symbolic).

+   *   **-regex regular expression**
+       *   Match the files with the filename specified in *regular expression*.

+   *   **-size n | b | c | w**
+       *   Match files with the size specified by *n*. By default, *n* refers to the file size in 512-byte blocks (**-size nb**). You can also specify bytes (**-size nc**), kilobytes (**-size nk**), or 2-byte words (**-size nw**).

+   *   **-type | b | c | d | f | l | p | s**
+       *   Match files of the specified type:
+           *   **b** Buffered block.
+           *   **c** Unbuffered character.
+           *   **d** Directory.
+           *   **f** Regular file (default).
+           *   **l** Symbolic link.
+           *   **p** Named pipe (FIFO).
+           *   **s** socket.

+   *   **-uid n**
+       *   Match files belonging to the user whose numerical ID is specified by *n*.

+   *   **-used n**
+       *   Match files last accessed *n* days after any of its attributes were last changed.

+   *   **-user username**
+       *   Match files belonging to the user specified by *username*.

+   *   **-xtype | b | c | d | f | l | p | s**
+       *   Match symbolic links of the specified type:
+           *   **b** Buffered block.
+           *   **c** Unbuffered character.
+           *   **d** Directory.
+           *   **f** Regular file (default).
+           *   **l** Symbolic link.
+           *   **p** Named pipe (FIFO).
+           *   **s** Socket.