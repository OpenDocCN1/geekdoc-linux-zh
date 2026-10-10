Node No: 1
…
Node No: 322
proc_file_read: Apparent buffer overflow!

As you can see, an overflow occurs after one page (4,096 in this case) worth of ASCII characters have been produced.

To handle such large procfs files, you need to refashion the code in Listing C.1 using the start parameter alluded to earlier. This makes the function somewhat complicated and is shown in Listing C.2. The semantics of this modified implementation is as follows:

+   • readme_proc() is called multiple times, each invocation yielding a maximum of count bytes starting at offset. The count requested during each call is less than the size of a page.

+   • During each invocation, the kernel increments offset by the number of bytes returned by the previous invocation.

+   • readme_proc() signals eof only if the amount of data produced is less than or equal to the requested count plus the current offset. If eof is not set, the function is called again with offset advanced by the number of bytes returned previously.

+   • After each invocation, only those bytes starting from *start are collected and returned to the caller.

Print the values of *start, offset, count, and page, and look at the output generated during each invocation to better understand the operation sequence.

With this hack, your procfs file can supply large amounts of data to user space without size limitations:

```
bash> cat /proc/readme
Node No: 0
Node No: 1
…
Node No: 499
```

# **Listing C.2. Large Procf s Reads**