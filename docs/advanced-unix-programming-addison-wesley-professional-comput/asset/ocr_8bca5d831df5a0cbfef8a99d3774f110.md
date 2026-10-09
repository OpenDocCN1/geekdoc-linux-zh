Aside from the obvious—being able to do in one system call what would otherwise take several—how much do `readv` and `writev` buy you? Table 2.4 shows some timing tests based on using `readv` to write 16 data items of 200 bytes each 50,000 times vs. substituting 16 calls to `write` for each call to `writev`. Thus, each test wrote a 160MB file. As the different UNIX systems were on different hardware, we’ve normalized the times to show the `writev` system time as 50 sec., which happens to be about what it was on the Linux machine.12

# **Table 2.4 Speed of `writev` vs. `write`**

| System Call | User | System |
| :--- | :--- | :--- |
| **Solaris** | | |
| `writev` | 1.35 | 50.00 |
| `write` | 8.45 | 67.61 |
| **Linux** | | |
| `writev` | .17 | 50.00 |
| `write` | 1.83 | 27.67 |
| **FreeBSD** | | |
| `writev` | .39 | 50.00 |
| `write` | 4.90 | 209.89 |

For Solaris and, especially, FreeBSD, it looks like `writev` really does win over `write`. On Linux the system time is actually *worse*. Reading through the Linux code to see why, it turns out that for files, *Linux* just loops through the vector, calling `write` for each element! For sockets, which are what `readv` and `writev` were designed for, Linux does much better, carrying the vector all the way down to some very low-level code. We don’t have timing tests to report, but it’s apparent from the code that on sockets `writev` is indeed worthwhile.

12. As you read the table, remember that you can’t conclude anything about the relative speeds of, say, Linux vs. FreeBSD, because each was separately normalized. We’re only interested in the degree to which each system provides an advantage of `writev` over `write`. Also, Linux may not be as bad as my results show; see www.basepath.com/asp/writer.htm.