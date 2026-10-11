+   3. Read one byte, line 61. For our purposes, `safe_read()` acts like `read()`; it’s explained in Section 10.4.4, “Restartable System Calls,” page 357.
+   4. Seek back to the front of the file with `lseek()`, line 62. This is done to write the just-read byte back on top of itself.
+   5. Write the byte back, line 63. `full_write()` acts like `write()`; it is also covered in Section 10.4.4, “Restartable System Calls,” page 357.
+   6. If the file is of zero size, use `ftruncate()` to set it to zero size (line 68). This doesn’t change the file, but it has the side effect of updating the access and modification times. (`ftruncate()` was described in Section 4.8, “Setting File Length,” page 114.)
+   7. Close the file, line 69.

These steps are all done in one long successive chain of tests, inside an `if`. The tests are set up so that if any operation fails, `utime_null()` returns −1, like a regular system call. `errno` is automatically set by the system, for use by higher-level code.

The `rpl_utime()` function (lines 75–82) is the “replacement `utime()`. ” If the second argument is not `NULL`, then it calls the real `utime()`. Otherwise, it calls `utime_null()`.

# 5.5.4 Using `fchown()` and `fchmod()` for Security

The original Unix systems had only `chown()` and `chmod()` system calls. However, on heavily loaded systems, these system calls are subject to race conditions, by which an attacker could arrange to replace with a different file the file whose ownership or permissions were being changed.

However, once a file is opened, race conditions aren’t an issue anymore. A program can use `stat()` on a pathname to obtain information about the file. If the information is what’s expected, then after the file is opened, `fstat()` can verify that the file is the same (by comparing the `st_dev` and `st_ino` fields of the “before” and “after” `struct stat` structures).

Once the program knows that the files are the same, the ownership or permissions can then be changed with `fchown()` or `fchmod()`.