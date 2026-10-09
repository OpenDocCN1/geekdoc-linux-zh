To see the great benefits of user buffering, Table 2.3 shows the times in seconds for the file copy using **BUFIO**, the standard I/O Library, and the straight-system-call method (shown in *copy2*).

**Table 2.3** Comparison of Buffered and Unbuffered I/O

| Method | User * | System | Total |
| :--- | :---: | :---: | :---: |
| **BUFIO** | | | |
| Solaris | 1.00 | 0.51 | 1.51 |
| Linux | 1.00 | 0.28 | 1.28 |
| FreeBSD | 1.00 | 0.45 | 1.45 |
| **Standard I/O** | | | |
| Solaris | 0.57 | 0.24 | 0.81 |
| Linux | 11.32 | 0.15 | 11.48 |
| FreeBSD | 1.02 | 0.20 | 1.22 |
| **BUFSIZ buffer** | | | |
| Solaris | 0.00 | 0.52 | 0.52 |
| Linux | 0.00 | 0.23 | 0.23 |
| FreeBSD | 0.01 | 0.37 | 0.38 |

* All times in seconds and normalized within systems so that user BUFIO time on that system is 1.00.

With user buffering we’ve almost got the best of both worlds: We process the data as we like, even 1 byte at a time, yet we achieve a system time about the same as the **BUFSIZ** buffer method. So user buffering is definitely the right approach. Except for Linux, the standard I/O times are the best; it does what our **BUFIO** functions do, except faster and with more flexibility. The standard I/O user time for Linux (11.32) sticks out. A bit of research showed that while we used the gcc