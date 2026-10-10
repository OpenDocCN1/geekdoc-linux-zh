Maximum: ``1`` (include System V IPC semaphore code in kernel)
Default: ``1``

Specify integer value of ``0`` or ``1``.

# Description

``sema`` determines whether the code for System V IPC semaphore is to be included in the kernel at system boot time (Series 700 systems only).

+   - ``sema`` = 1 Code is included in the kernel (enable IPC shared memory).

+   - ``sema`` = 0 Code is not included in the kernel (disable IPC shared memory).

Series 800 systems: IPC shared memory is always enabled in the kernel.

Series 700 systems: If ``shmrem`` is set to zero, all other IPC shared memory parameters are ignored.

Starbase graphics library and some other HP-UX subsystems use semaphores. Disable only if you are certain that no applications on your system depend on System V IPC semaphores.

If ``sema`` is zero, any program that uses ``semget()`` or ``semop()`` system calls, will return a ``SIGSYS`` signal.

# semaem

Define the maximum amount a semaphore value can be changed by a semaphore `undo` operation.

Acceptable Values:

+   - Minimum: ``0``
+   - Maximum: ``SEMVMX`` or 32767, whichever is smaller``
+   - Default: ``16384``

Specify integer value or use integer formula expression.

# Description

An !<undo!> is an optional flag in a semaphore operation which causes that operation to be undone if the process which invoked it dies.