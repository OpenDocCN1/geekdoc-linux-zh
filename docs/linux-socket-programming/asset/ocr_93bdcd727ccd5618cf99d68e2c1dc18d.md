With the blocking style, the program waits until data arrives. The polling style repeatedly calls the recv() system call until the data arrives. The timeout style, on the other hand, may not get the data if the data does not arrive in time. Still, with the timeout style, you do not lose the message; the kernel holds it for you until you call for it again. Lastly, with the asynchronous style, the kernel notifies the task when it gets data.

Notice that it’s a different story with how each style handles the interface when you send a message. The kernel’s buffers take up the slack to speed up the processing in a nonblocking call. In all cases, a blocking call stops until the kernel completely sends the message. (This is not completely true, since the kernel really waits until it can send the message before waking the task, but to simplify programming you can assume that the message is gone when the task resumes.) Polling and asynchronous calls store the message in the buffers and return immediately. Figure 8.2 assumes that the data is too large to store entirely in the buffers.

# Figure 8.2. The write operation offers more time to the task by using buffers.

![](bbox=[0.17, 0.34, 0.81, 0.66])

The following sections show you how to use polling, timeout, and asynchronous I/O.

# Polling I/O

The program may have several things to do besides waiting for a packet. Once you call send() to send a message, it’s not a concern how or when the message leaves the computer. As far as you are concerned, the I/O subsystem sends the message complete and intact. Often this is not the case; most messages are chopped up to fit the limitations of the network. Similarly, you may not want to get pieces of a message. Instead, you want to fill your buffer. In both cases, your program stops and waits for the task to finish.

Polling helps you avoid being blocked in I/O communication by checking to see if the channel is ready. To use polling, configure the channel for nonblocking. Then, check the return value of a system call. If the call returns EWOULDBLK (or EAGAIN), try again a little later. Programs often place