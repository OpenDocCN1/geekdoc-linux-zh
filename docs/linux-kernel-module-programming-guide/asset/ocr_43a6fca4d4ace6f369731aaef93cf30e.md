kernel (of course, location is readable by user processes, it is not writable by), and then
Under Intel CPUs, this is done by means of interrupt 0x80. The hardware knows that
you jump to this location, you are no longer running in restricted user mode, but as the
operating system kernel — and therefore you are allowed to do whatever you want.

The location in the kernel process is called system_call. The pro-
jecture at that location checks the call number, which tells the kernel what service
the process requested. Then, it looks at the table of system calls (sys_call_table)
to see the address of it. Then it calls the function, and af-	er returns, it does a few system checks and then return back to the process (or a-
different process, if the process ran out). If you want to read this code, it is
the source file arch/<architecture>/kernel/entry.S, after the line EN-\TRY(system_call).

So, if we want to change a certain system call, what we need to do is
write our function to implement it (usually by adding a bit of our own code and then
calling the original function) and then change the pointer to sys_call_table to point to
out function. Because we might be removed and we don't want to leave the system in
unstable state, it is important for cleanup_module to restore the table to its original
state.

The source code is an example of such a kernel module. We want to 'spy' on
certain user, and to print a message when that user opens a file. To this ends, we
replace the system call to open a file with our own function, called our_sys_open.
this function checks the uid (user's id) of the current process, and if it's equal to the uid
we spy on, it calls print to display the name of the file to be opened. Then, either,
it calls the original open function with the same parameters, to actually open the.

The init_module function replaces the appropriate location in sys_call_table
and keeps the original pointer in a variable. The cleanup_module functions uses
variable to restore everything back to normal. This approach is dangerous, because of
tossibility of two kernel modules changing the same system call. Imagine we have two
kernel modules, A and B. An open system call will be A_open and B's will be B_open.
Now, when A is inserted into the kernel, the system call is replaced with A_open, which
calls the original sys_open when it's done. Next, B is inserted into the kernel, which
replaces the system call with B_open, which will call what it thinks the original system
call, A_open, when it's done.

Now, if B is removed first, everything will be well — it will simply restore the system
call to A_open, which calls the original. However, if A is removed and then B is removed,
the system will crash. A removal will restore the system call to the original, sys_open,

![](bbox=[0.118, 0.843, 0.679, 0.915])