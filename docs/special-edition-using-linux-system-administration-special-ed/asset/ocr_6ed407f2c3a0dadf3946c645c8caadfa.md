**TABLE 12.1 CONTINUED**

| Server Type | Disk | CPU | Memory | Network | Comments |
|---|---|---|---|---|---|
| DNS |  |  |  |  | DNS servers require little in the way of hardware resources. |
| FTP |  |  | X | X | Generally, FTP servers do not require large systems except in the most extreme situations and place small demands on hardware. |
| X Application |  | X | X | X | X is CPU, memory, network bound. |
| Server Mail | X |  | X |  | sendmail makes extensive use of disks for writing temporary files and requires considerable memory to handle open connections. |
| Web (Static Files) |  |  | X | X | Serving static files places little pressure on disk and CPU. Memory and network bandwidth are the primary bottlenecks. |
| Web (Dynamic Content) |  |  | X | X | Memory and CPU critical for good dynamic content performance on a Web server. |
| Web (Search Engine) | X |  | X | X | Web search require considerable disk performance. |

# DATABASE SERVER CONSIDERATIONS

Before trying to estimate the capacity of a database server, you must understand the variables that govern a database application. When these variables and their relationships to each other are better understood, it is easier to arrive at capacity numbers.

In order to optimize the performance of a database application such as Oracle on a Linux system, three areas need attention: