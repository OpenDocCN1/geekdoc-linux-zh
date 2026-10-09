link programs.

The MPICH implementation of MPI provides instructions on setting up a make-file or project file for use with Microsoft Visual Studio. In version 1.2.1, these are

+   * **Include Path:** '<MPICH home>\\include' 
+   * **Switches:** /MTd for the debug version and /MT for the release version 
+   * **Libraries:** 'mpich.lib' (contains MPI-1, all PMPI routines, and MPI-IO); 'mpe.lib' contains the profiling interface to MPI-1 
+   * **Library Path:** '<MPICH home>\\lib' 
+   * **Include path:** '<MPICH home>\\include'

Running an MPI program (in most implementations) also requires a special program, particularly when parallel programs are started by a batch system as described in Chapter 13. Many implementations provide a program **mpirun** that can be used to start MPI programs. For example, the command

```
mpirun -np 4 helloworld
```

runs the program **helloworld** using four processes. Most MPI implementations will attempt to run each process on a different processor; most MPI implementations provide a way to select particular processors for each MPI process. In MPICH, **mpirun** should be run from within a console process.

The name and command-line arguments of the program that starts MPI programs were not specified by the original MPI standard, just as the C standard does not specify how to start C programs. However, the MPI Forum did recommend, as part of the MPI-2 standard, an **mpiexec** command and standard command-line arguments to be used in starting MPI programs. By 2002, most MPI implementations should provide **mpiexec**. This name was selected because no MPI implementation was using it (many are using **mpirun**, but with incompatible arguments). The syntax is almost the same as for the MPICH version of **mpirun**; instead of using **-np** to specify the number of processes, the switch **-n** is used:

```
mpiexec -n 4 helloworld
```

The MPI standard defines additional switches for **mpiexec**; for more details, see Section 4.1, “Portable MPI Process Startup”, in the MPI-2 standard.