(see restart-example.c on the Web site). Before doing this, you must manually terminate all current processes under the older parent. (You may have to use this restarting technique on all signals that can terminate your server.)

# SIGIO

You can get a performance boost to your network program by offloading the I/O notification to the kernel. When implemented correctly, your program gets the SIGIO signal whenever the I/O buffers no longer block a read or write operation. For writing, this occurs when the I/O subsystem can accept at least one byte (see the write low water mark, SO_SNDBUFOAT, socket option). For reading, this occurs when the I/O subsystem has received at least one byte (see the read low water mark, SO_RCVLOWAT, socket option). See Chapter 8, “Choosing when to Wait for I/O,” for how to implement this signal, and see Chapter 9 for performance benefits.

# SIGALRM

Like the SIGIO signal, you only get the SIGALRM signal if your program asked for it. This signal is typically the result of calling alarm() system call, a time-delayed wakeup call. Daemons often use this signal as a watchdog to ensure that the program is still alive or to check the solidity of the connection. See Chapter 9 for using this as a connection heartbeat checker.

# Resource Management

Signals are one small part of a program’s resources. If you track and capture specific signals, you can reduce system corruption and may be able to increase performance. The whole program has much more than just signals. It includes files, heap, static/dated memory, and CPU time. You have additional resources, such as child processes and shared memory. What makes a reliable server (or even client) is being careful with your resources.

# File Management

Your program automatically gets three standard files when it starts up: stdin, stdout, and stderr. You should be familiar with these and the fact that the user can redirect any one of them. This is typically not a problem because the kernel flushes and closes these for you upon program termination.

New files and sockets are a different matter. You must remember to track and close each file. Even though the kernel closes all files for you upon program termination (such as the standard I/O files), all files require a portion of the kernel’s and program’s memories. All files that the program loses track of chew up more and more resources.

Even if you are working with one file, it is good programming practice to force a close somewhere in the program. Someday, in the course of revision, you may open more files.