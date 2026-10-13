+   - **semvmx** — Maximum value of a semaphore. Because of the interaction with undo structures and semaem (more details below), this tunable should not exceed a maximum of its default value of 32767 unless you can guarantee that SEM_UNDO is never being used. The actual value of a semaphore is stored as an unsigned short (2 bytes) in its semaphore structure, implying that the maximum semaphore value can be 65535 (64 Kbytes), the maximum value of an unsigned short data type. The next bullet explains why the limit should really be 32767.

+   - **semaem** — Maximum adjust-on-exit value. This value is stored as an integer in the seminfo structure that the kernel uses to maintain the tunable values, but it is implemented as a signed short in the undo structure. It needs to be signed because semaphore operations can increment or decrement the value of a semaphore, and thus the system might need to apply a negative or positive adjustment value to do a successful adjust-on-exit operation.
+   
+     The actual value of a semaphore can never be negative. The maximum value for a signed short, which is 2 bytes (16 bits), is 32767 (32 Kbytes). If semvmx were set to 65535 and the application actually set semaphore values that high, the system would not be able to undo the entire range of semaphore value changes, because semaem can never be greater than 32767. This is why semvmx should never be greater than 32767, unless you don’t care about undo operations.

# 10.3.2 Kernel Implementation of System V Semaphores

During initialization of the semaphore code, when /kernel/sys/semsys is first loaded, the value of semmni is checked to ensure it is not greater than the maximum allowable value of 65536 (64 Kbytes). If it is, it gets set to 65536 and a console message is printed stating that the value of semmni was too large. Following that, the tunable parameters, with the exception of semusz, from the /etc/system file are plugged into the internal seminfo data structure.

Just as with shared memory, the system checks for the maximum amount of available kernel memory and divides that number by 4, to prevent semaphore requirements from taking more than 25 percent of available kernel memory. Actual memory requirements for semaphores are calculated as follows.

```
total_kernel_memory_required =
        (semms * (sem structure size) +
         (semms * (semid_ds structure size) +
         (semms * (kernel mutex size)) +
         (max_nprocs * (undo structure size)) +
         (semsz * (semmnu * (integer size)))
```

The structure sizes are given in the previous section. Pointers and integers are 4 bytes, and a kernel mutex is 8 bytes. The maximum process value is determined