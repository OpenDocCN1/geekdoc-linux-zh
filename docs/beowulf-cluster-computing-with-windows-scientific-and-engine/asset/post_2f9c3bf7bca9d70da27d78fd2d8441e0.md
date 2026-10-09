
particular, the Class W problems can easily be run on a single-processor system. For a Beowulf system with, say, 32 processors, the Class A problems are an appropriate test. The Class B problems are appropriate for systems with roughly 32–128 processors. The Class C problems can be used for systems with up to 256 CPUs.

Unfortunately, almost the entire NASA research team that designed and championed the NPB suite has now left NASA. As a result, NASA is no longer actively supporting and promoting the benchmarks. Thus, there probably will not be any larger problem sets developed. Further, NASA is no longer actively collecting results.

The NPB suite does, however, continue to attract attention from the parallel computing research community. This is because the suite reflects real-world parallel scientific computation to a significantly greater degree than do most other available benchmarks.

We recommend that users of Beowulf-type systems use the MPI version of the NPB suite. Instructions for downloading, installing, and running the suite are given at the NPB Web site.

## II PARALLEL PROGRAMMING

### 9 Parallel Programming with MPI

William Gropp and Ewing Lusk

Parallel computation on a Beowulf is accomplished by dividing a computation into parts and making use of multiple processes, each executing on a separate processor, to carry out these parts. Sometimes an ordinary program can be used by all the processes, but with distinct input files or parameters. In such a situation, no communication occurs among the separate tasks. When the power of a parallel computer is needed to attack a large problem with a more complex structure, however, such communication is necessary.

One of the most straightforward approaches to communication is to have the processes coordinate their activities by sending and receiving messages, much as a group of people might cooperate to perform a complex task. This approach to achieving parallelism is called *message passing*.

In this chapter and the next, we show how to write parallel programs using MPI, the Message Passing Interface. MPI is a message-passing library specification. All three parts of this description are significant.

- MPI addresses the message-passing model of parallel computation, in which processes with separate address spaces synchronize with one another and move data from the address space of one process to that of another by sending and receiving messages.[^1]
- MPI specifies a library interface, that is, a collection of subroutines and their arguments. It is not a language; rather, MPI routines are called from programs written in conventional languages such as Fortran, C, and C++.
- MPI is a specification, not a particular implementation. The specification was created by the MPI Forum, a group of parallel computer vendors, computer scientists, and users who came together to cooperatively work out a community standard. The first phase of meetings resulted in a release of the standard in 1994 that is sometimes referred to as MPI-1. Once the standard was implemented and in wide use a second series of meetings resulted in a set of extensions, referred to as MPI-2. MPI refers to both MPI-1 and MPI-2.

As a specification, MPI is defined by a standards document, the way C, Fortran, or POSIX are defined. The MPI standards documents are available at `www.mpi-forum.org` and may be freely downloaded. The MPI-1 and MPI-2 standards are also available as journal issues [10, 11] and in annotated form as books in this series [14, 4]. Implementations of MPI are available for almost all parallel computers, from clusters to the largest and most powerful parallel computers in the world. In Section 9.8 we provide a summary of the most popular cluster implementations.

A goal of the MPI Forum was to create a powerful, flexible library that could be implemented efficiently on the largest computers and provide a tool to attack the most difficult problems in parallel computing. It does not always do the simplest things in the simplest way but comes into its own as more complex functionality is needed. In this chapter and the next we work through a set of examples, starting with the simplest.

#### 9.1 Hello World in MPI

To see what an MPI program looks like, we start with the classic “hello world” program. MPI specifies only the library calls to be used in a C, Fortran, or C++ program; consequently, all of the capabilities of the language are available. The simplest “Hello World” program is shown in Figure 9.1.

```
#include "mpi.h"
#include <stdio.h>

int main( int argc, char *argv[] )
{
    MPI_Init( &argc, &argv );
    printf( "Hello World\n" );
    MPI_Finalize();
    return 0;
}
```

![](img/e2283ffaea56e577ac05056b4bb738fc_197_0.png)

All MPI programs must contain one call to **MPI_Init** and one to **MPI_Finalize**. All other[^2] MPI routines must be called after **MPI_Init** and before **MPI_Finalize**. All C and C++ programs must also include the file `mpi.h`; Fortran programs must either use the **MPI** module or include **mpif.h**.

The simple program in Figure 9.1 is not very interesting. In particular, all processes print the same text. A more interesting version has each process identify itself. This version, shown in Figure 9.2, illustrates several important points. Of particular note are the variables rank and size. Because MPI programs are made up of communicating processes, each process has its own set of variables. In this case, each process has its own address space containing its own variables rank and size (and argc, argv, etc.). The routine MPI_Comm_size returns the number of processes in the MPI job in the second argument. Each of the MPI processes is identified by a number, called the rank, ranging from zero to the value of size minus one. The routine MPI_Comm_rank returns in the second argument the rank of the process. The output of this program might look something like the following:

- Hello World from process 0 of 4
- Hello World from process 2 of 4
- Hello World from process 3 of 4
- Hello World from process 1 of 4

Note that the output is not ordered from processes 0 to 3. MPI does not specify the behavior of other runtimes or language statements such as printf; in particular, it does not specify the order of output from print statements.

#### 9.1.1 Compiling and Running MPI Programs

The MPI standard does not specify how to compile and link programs (neither do C or Fortran). However, most MPI implementations provide tools to compile and link programs.

The MPICH implementation of MPI provides instructions on setting up a make-file or project file for use with Microsoft Visual Studio. In version 1.2.1, these are:

- **Include Path:** '<MPICH home>\include'
- **Switches:** /MTd for the debug version and /MT for the release version
- **Libraries:** 'mpich.lib' (contains MPI-1, all PMPI routines, and MPI-IO); 'mpe.lib' contains the profiling interface to MPI-1
- **Library Path:** '<MPICH home>\lib'

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

[^1]: Processes may be single threaded, with one program counter, or multithreaded, with multiple program counters. MPI is for communication among processes rather than threads. Signal handlers can be thought of as executing in a separate thread.
[^2]: There are a few exceptions, including **MPI_Initialized**.
