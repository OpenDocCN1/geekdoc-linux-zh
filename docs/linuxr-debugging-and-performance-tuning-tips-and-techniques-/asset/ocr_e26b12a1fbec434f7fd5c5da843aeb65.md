+   The tree API is an additional set of data storage and search functions that maintains data in binary trees, the effect of which is to keep data sorted. The tree API is very flexible, allowing use of multiple trees and arbitrary data.

# Exercises

+   Write the lockf() function, using fcntl() to do the locking.

+   The directory /usr/src/linux/Documentation contains a number of files that describe different aspects of the operating system’s behavior. Read the files locks.txt and mandatory.txt for more information about Linux’s handling of file locks.

+   Run the ch14-lockall program on your system, without mandatory locking, and see if you can change the operand file.

+   If you have a non-Linux system that supports mandatory locking, try the ch14-lockall program on it.

+   Write a function named strftimes(), with the following API:
+   
+   ```
+   size_t strftimes(char *buf, size_t size, const char *format,
+             const struct timespec *tp);
+   ```
+   
+   It should behave like the standard strftime() function, except that it allows %q to mean “the current number of microseconds.”

+   Using the strftimes() function you just wrote, write an enhanced version of date that accepts a format string beginning with a leading + and formats the current date and time. (See date(1).)

+   The handling of the timeout in ch14-timers.c is rather primitive. Rewrite the program to use setjmp() after printing the prompt and longjmp() from within the signal handler. Does this improve the structure or clarity of the program?

+   We noted that ch14-timers.c contains a deliberate race condition. Suppose the user enters a response within the right time period, but ch14-timers is suspended before the alarm can be canceled. What call can you make to cut down the size of the problem window?

+   Draw the tree as shown by the output of ch14-tsearch in Section 14.4.5, “Tree Traversal: twalk(),” page 557.