# 11.2 Program Examples

In this section we discuss several complete PVM programs in detail. The first example, forkjoin.c, shows how to spawn off processes and synchronize with them. We then discuss a Fortran dot product program PSDOT.F and a matrix multiply example. Lastly, we show how PVM can be used to compute heat diffusion through a wire.

# 11.3 Fork/Join

The fork/join example demonstrates how to spawn off PVM tasks and synchronize with them. The program spawns several tasks, three by default. The children then synchronize by sending a message to their parent task. The parent receives a message from each of the spawned tasks and prints out information about the message from the child tasks.

This program contains the code for both the parent and the child tasks. Let’s examine it in more detail. The very first thing the program does is call pvm_mytid(). In fork/join we check the value of mytid; if it is negative, indicating an error, we call pvm_error() and exit the program. The pvm_error() call will print a message indicating what went wrong with the last PVM call. In this case the last call was pvm_mytid(), so pvm_error() might print a message indicating that PVM hasn’t been started on this machine. The argument to pvm_error() is a string that will be prepended to any error message printed by pvm_error(). In this case we pass argv[0], which is the name of the program as it was typed on the command-line.

Assuming we obtained a valid result after the Unix perror() function.

Assuming we obtained a valid result after the Unix pcall myid, we now call pvm_parent(). The pvm_parent() function will return the tid of the task that spawned the calling task. Since we run the initial forkjoin program from a command prompt, this initial task will not have a parent; it will not have been spawned by some other PVM task but will have been started manually by the user. For the initial fork/join task the result of pvm_parent() will not be any particular task id but an error code, PvmNoParent. Thus we can distinguish the parent fork/join task from the children by checking whether the result of the pvm_parent() call is equal to PvmNoParent. If this task is the parent, then it must spawn the children. If it is not the parent, then it must send a message to the parent.

Let’s examine the code executed by the parent task. The number of tasks is taken from the command-line as argv[1]. If the number of tasks is not legal then we