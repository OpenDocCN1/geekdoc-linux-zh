+   - What should I do if a process (such as P1) needs more memory to execute?

+   - When will the process receive information about the specific physical memory address, which memory will start executing it, and how should the memory addresses used in its code be converted?

+   - What should I do if the process doesn't need all the memory allocated to it?

Direct loading of processes into physical memory does not provide an answer to these questions. Obviously, some memory translation tools are needed to allow processes to use address sets that are different from physical memory addresses. Before we understand the peculiarities of these addresses, let us briefly dwell on the peculiarities of composing and downloading applications.

The program usually resides on disk as a binary executable file obtained after compilation and layout. It must be loaded into memory (process address space) for its execution. Modern architectures allow processes to be located anywhere in physical memory, and the same program can accommodate different processes loaded into different memory locations. It is unknown in advance which memory area the program will be loaded into.

During execution, the process accesses different addresses, in particular, when a function is called, it uses its address (this is the code address), and the global variable accesses the memory address to store the value of that variable (this is the data address).

The programmer does not normally use memory addresses directly in his program, instead, they use symbolic names (functions, global variables, etc.). Due to compilation and layout, these names are linked to moving addresses (such addresses are specified in relative units, such as "100 bytes from the beginning of the module"). When running the program, the relocated addresses, in turn, are bound to absolute addresses in memory. In fact, each bind is a mapping of one set of addresses to another.