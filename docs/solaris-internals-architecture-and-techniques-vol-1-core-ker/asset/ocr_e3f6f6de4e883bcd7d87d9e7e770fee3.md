door descriptor (door_desc), used for passing door descriptors when a door function is called.

To continue: A call to door_create(3X) enters the libdoor.so library door_create() entry point (as is the case with any library call).

+   The kernel door_create() is invoked from the library and performs the following actions:

+   - Allocates kernel memory for door_node and initializes several fields of door_node and the door vnode (part of the door_node structure).

+   - Links the door_target field to the process structure of the calling kernel thread.

+   - Sets door_pc, a function pointer, to the address of the function served by the door (the code that will execute when a client calls door_call(3X)).

+   - Sets door_flags as directed by the attributes passed by the caller.

+   - Initializes the vnode mutex lock (v_lock) and condition variable (v_cv). Initializes several other fields in the vnode to specify the vnode type (VDOR) and references to the vnode operations and virtual file system (VFS) switch table entries of the doorfs file system.

+   - Adds the door_node to the process's door list (p_door_list) and allocates a file descriptor for the door descriptor by means of the kernel falloc() function, which allocates a file structure and user file descriptor.

+   - The kernel door_create() now completed, the code returns to the libdoor.so door_create() code.

+   - The library makes sure that the calling process has been linked with the Solaris threads library, libthread.so and returns an error if the link has not been made.

A door server requires linking with libthread.so because the door code uses the threads library interfaces to create and manage a pool of door server threads.

+   - The last thing the library-level door_create() code does is call thr_create(3T) to create a server thread for the door server, as an execution resource for calls into the function exported by the door.

+   - thr_create(3T) creates a detached, bound thread that executes the library door_create_func() routine, which disables cancellation of the current thread (pthread_setcancelstate(3T)) and enters the kernel door_return() code.