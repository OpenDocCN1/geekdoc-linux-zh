# 18.7.4 System Call Failure and Error Handling

A UNIX system call returns -1 on failure. Thus, while using a system call in your code, you must first check whether the call has failed and use appropriate code to handle it. In most cases, you would like to display an adequate error message to the user by using the C Standard Library function perror() and terminate the program execution by using the exit() system call.

# EXERCISE 18.4

Browse through <stdio.h> and identify the number of functions and macros defined in it.

# EXERCISE 18.5

List the Standard I/O library calls for character and file processing. Give a one-sentence description of each call.

# 18.8 FILE MANIPULATION

In this section, we discuss the UNIX system calls to access and manipulate file data and attributes. Our focus will be on the following operations:

+   - Opening a file
+   - Creating a file
+   - Reading file data
+   - Writing data to a file
+   - Positioning the read/write file pointer for random access
+   - Truncating a file
+   - Closing a file
+   - Checking the existence of a file
+   - Removing a file
+   - Obtaining and displaying file attributes

We will primarily focus on manipulating data in regular files. However, we discuss the access, display, and modification of file attributes for files of all types. We do not discuss the manipulation of directories, but briefly describe the system call interface for doing so. The system calls for handling sockets and FIFOs are described in detail in Chapters 20 and 21.

# 18.8.1 Opening and Creating a File

You can use the open() system call to open an existing file for reading, writing, or performing both operations. If a file does not exist, you can create it and open it for writing by