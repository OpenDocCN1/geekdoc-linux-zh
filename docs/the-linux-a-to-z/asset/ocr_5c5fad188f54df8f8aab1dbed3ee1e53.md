![](bbox=[0.28, 0.12, 0.78, 0.65])

Figure 29.2 Stack layout in twice() just before return.

next on the stack, with the ebp register set to point to this stack location, the stack locations set aside for the local variables x and y, the current position of the stack pointer, and the value of 6, assigned to the variable x on the stack.

The second snap-shot (see Figure 29.2) is taken at the end of the twice() function, just before the execution of the return statement. It shows that, after the stack frame for the main() function, the value 6 was pushed onto the stack (as the value of the parameter passed into the twice() function), which was later labeled with the name n. After this, the machine code call to the function twice() caused another return address to be pushed onto the stack. This was followed by stacking the value in ebp and updating the ebp register to point to the saved value. By this mechanism, the ebp register has effectively been set up as the head pointer to a linked list of function stack frames, all stored on the stack. Finally, the variable r is allocated space on the stack to which the calculation subsequently assigns the value 12.

# 29.3 Thread Scheduling

Remember that all the threads within a single process share the program and all the global environment of the process. The only private parts of a thread are the contents of any significant processor registers and the stack, which it uses during