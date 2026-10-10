within the kernel are said to be operating in *kernel context*, while application programs are said to operate in *user space context*. A user space process can access only memory it owns, and uses kernel system calls to access privileged resources such as file and device I/O. An example might make this more clear.

Consider an application that opens a file and issues a read request (see Figure 2-6). The read function call begins in user space, in the C library read( ) function. The C library then issues a read request to the kernel. The read request results in a context switch from the user's program to the kernel, to service the request for the file's data. Inside the kernel, the read request results in a hard-drive access requesting the sectors containing the file's data.

![](bbox=[0.05, 0.36, 0.8, 0.78])

# **FIGURE 2-6**
Simple file read request

Usually the hard-drive read is issued asynchronously to the hardware itself. That is, the request is posted to the hardware, and when the data is ready, the hardware interrupts the processor. The application program waiting for the data