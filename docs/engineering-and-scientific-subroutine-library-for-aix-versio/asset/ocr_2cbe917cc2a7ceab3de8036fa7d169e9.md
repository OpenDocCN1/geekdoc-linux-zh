# Creating Multiple Threads and Calling ESSL from Your C Program

The example shown below shows how to create two threads, where each thread calls the ISAMAX subroutine. To use the AIX pthreads library, you must specify the pthread.h header file as the first include file in your program.

Note: Be sure to compile this program with the cc\_r command.