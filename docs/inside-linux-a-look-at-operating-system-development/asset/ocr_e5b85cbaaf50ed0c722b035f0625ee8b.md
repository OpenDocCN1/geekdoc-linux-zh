# Appendix B

# System Calls

Most system calls are ultimately accessed by an entry point in a jump table inside the kernel, but the user knows them by entry points in the run-time library. (Here we’re treading on soft ground. Hidden calls can bypass the run-time library and perform the trap instruction directly. This is a common procedure when some new call is being tested. When it proves correct and useful, the entry points will be added to the run-time library.) At this moment, there are 162 entry points in the jump table and 172 documented entry points in the run-time library. (But my library is slightly out of date, so some of the system calls do have a run-time library equivalent.)

+   * **I/O —** Although the brief descriptions often refer to “a file”, the file may actually be a reference to a directory, a peripheral device, a fifo, or other such object.

+     - **Universal**
+     * access - Check user’s permissions for a file
+     * chmod, fchmod - Change permissions of a file
+     * chown, fchown - Change ownership of a file
+     * close - Close a file descriptor
+     * dup, dup2 - Duplicate a file descriptor
+     * fcntl - Manipulate file descriptor
+     * link - Make a new name for a file