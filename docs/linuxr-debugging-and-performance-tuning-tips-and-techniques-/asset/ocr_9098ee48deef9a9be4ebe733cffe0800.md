buffer returned (line 84), breaking the infinite loop. This ensures that the entire link contents have been placed into the buffer, since readlink() has no way to indicate "insufficient space in buffer."

Lines 87–88 free the buffer and double the buffer size for the next try at the top of the loop. Lines 89–90 handle the case in which the link's size is too big: buf_size is greater than $SIZE_MAX, or $SIZE_MAX is larger than the value that can be represented in a signed integer of the same size as used to hold $SIZE_MAX and buf_size has wrapped around to zero. (These are unlikely conditions, but strange things do happen.) If either condition is true, the program dies with an error message. Otherwise, the function continues around to the top of the loop to make another try at allocating a buffer and reading the link.

Some further explanation: The `$SIZE_MAX / 2 < $SIZE_MAX$` condition is true only on systems on which `$SIZE_MAX < 2 * $SIZE_MAX$`; we don't know of any, but only on such a system can buf_size wrap around to zero. Since in practice this condition can't be true, the compiler can optimize away the whole expression, including the following `buf_size == 0` test. After reading this code, you might ask, "Why not use lstat() to retrieve the size of the symbolic link, allocate a buffer of the right size with malloc(), and be done?" Well, there are a number of reasons.9

+   • `lstat()` is a system call— it's best to avoid the overhead of making it since the contents of most symbolic links will fit in the initial buffer size of 128.

+   • Calling `lstat()` introduces a race condition: The link could change between the execution of `lstat()` and `readlink()`, forcing the need to iterate anyway.

+   • Some systems don't properly fill in the `st_size` member for symbolic links. (Sad, but true.) In a similar fashion, as we see in Section 8.4.2, "Getting the Current Directory: getcwd()," page 258, Linux provides special symbolic links under `/proc` whose `st_size` is zero, but for which `readlink()` does return valid content.

Finally, when the buffer isn't big enough, `xreadlink()` uses `free()` and `malloc()` with a bigger size, instead of `realloc()`, to avoid the useless copying that `realloc()`

> 9 Thanks to Jim Meyer for explaining the issues.