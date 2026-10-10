"semmax" defines the system-wide maximum total number of individual semaphores that can be made available to system users.

When the free-space map shows that there are not enough contiguous semaphore slots in the semaphore area of shared memory to satisfy a "semget()" request, "semget()" returns a "ENOSPC" error. This error can occur even though there may be enough free semaphores slots, but they are not contiguous.

# semmsu

Define the maximum number of processes that can have undo operations pending on any given IPC semaphore on the system.

+   Acceptable Values:
+   
+   Minimum: 	"1"
+   Maximum: 	"nproc*4"
+   Default: 	"30"

Specify integer value.

Description

An !<undo!! is a special, optional, flag in a semaphore operation which causes that operation to be undone if the process which invoked it terminates.

"semmsu" specifies the maximum number of processes that can have undo operations pending on a given semaphore. It determines the size of the "sem_undo" structure.

A "semop()" system call using the "SEM_UNDO" flag returns an "ENOSPC" error if this limit is exceeded.

# semmap

Specify size of the free-space resource map used for allocating new System V IPC semaphores in shared memory.

+   Acceptable Values:
+   
+   Minimum: 	"4"
+   Maximum: 	Memory limited
+   Default: 	"SemMIN+2"