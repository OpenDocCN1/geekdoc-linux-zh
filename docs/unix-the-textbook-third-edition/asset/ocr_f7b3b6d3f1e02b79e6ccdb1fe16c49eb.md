6. What happens to a reader process when it reads from a pipe that has no data in it? Explain the reason for your answer.

7. What happens to a writer process when it writes to a full pipe? Explain the reason for your answer.

8. What is the effect of using the following flags in the pipe2() system call?
a. O_CLOEXEC
b. O_NONBLOCK

9. How should the pipe2() system call be used so that it behaves like the pipe() system call?

10. What is the synchronization issue in the bounded-buffer reader–writer problem? Who handles synchronization when two UNIX processes communicate with each other using pipes: the reader process, the writer process, or someone else (specify)?

11. Write a program that demonstrates how the reader and writer processes behave while communicating through a widowed pipe.

12. Write a C program, widowed.c, that creates a widowed pipe and demonstrates that when a process reads from a pipe that cannot be written to, it results in the reader process receiving the eof message.

13. When you compile and run the broken_pipe.c program in Section 20.4.2 on a Solaris machine, it terminates without generating the "Broken pipe" error message. How can you verify that the pipe was actually widowed and the program terminated when the write() system call was executed?

14. Use signal handling to generate the "Broken pipe" error message by the broken_pipe.c program when you compile and run it on a Solaris machine. Write two versions of the program. The first version should terminate the program after displaying the "Broken pipe" message and the second version should continue after displaying the message and execute the statement after the write() system call that causes SIGPIPE. Hint: Use signal().

15. Write a C program to demonstrate that a widowed pipe with its write end closed sends the eof message to the reader process. Show compilation and execution of the program.

16. Write a program that takes two command line arguments: the name of a text file that contains single-digit integer data and an integer to be searched from the sorted version of the data in the file. The program creates two children processes. The first child process reads the text file passed as the first argument, sorts the numbers (any sorting algorithm is allowed), and communicates the sorted numbers to the second child process via a pipe and exits. The second child process searches for the "majority number" in the sorted list of numbers, displays the majority number and sends the