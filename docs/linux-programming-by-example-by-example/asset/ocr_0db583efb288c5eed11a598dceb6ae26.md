Having added `syslog`'s logging functionality, if you try to execute the program as a normal user, `lpdated` will write an entry to the system log (usually `/var/log/messages` on Linux systems) resembling the following:

> Sep 14 21:12:04 hoser lpdated[8192]: open

This log entry indicates that at the date and time specified, on the host named `hoser`, a program named `lpdated`, with a PID of 8192, entered the text `open` into the system log. Referring to `lpdated`'s source code, you would be able to see where the error occurred.

All the error messages `lpdated` generates will be logged to the system log, although the timestamps themselves will still be written to `/var/log/lpdated.log`. The output that follows, taken from the system log, was generated because a non-root user attempted to run the program. The number in brackets is `lpdated`'s PID.

![](bbox=[0.046, 0.335, 0.13, 0.383])

# Output

> Jul 28 11:34:06 hoser lpdated[8895]: open

# What's Next?

This chapter discussed creating *daemons*, which are background programs that are always running and usually provide some sort of service. This completes the book's coverage of system programming topics. With your knowledge of basic development tools, covered in Part I, "The Linux Programming Environment," and a solid understanding of low-level system programming (covered in Part II, "System Programming"), you are ready to learn some of Linux's most common APIs, or application programming interfaces, in Part III, "Linux APIs."