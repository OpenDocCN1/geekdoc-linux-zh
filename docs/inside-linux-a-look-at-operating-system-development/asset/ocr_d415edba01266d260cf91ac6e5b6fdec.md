privileges. As a consequence, systems generally partition the matrix into orthogonal areas of interest to reduce storage requirements.

For instance, process control and file access are independent. This results in one of the new matrices being limited to processes accessing files as shown in Figure 4.23. Other agents and objects have been left out of this matrix.

![](bbox=[0.17, 0.29, 0.87, 0.51])

The sparse access matrix can be compressed in one or more dimensions. One common method is to reduce it to a single dimension indexed by the process. (We are in effect considering individual rows of the matrix shown in Figure 4.23.) A *capability list* consists of a list of files and what operations may be performed on each. The example in Figure 4.24 shows that process 2 can read file 1, read and write file 2, etc. Each process has such a list it shows exactly what a process can do to any given file.

The access matrix could instead be compressed to a single dimension indexed by the file or directory. Each element of this array is called an *access control list* and consists of a list of processes and what each may do with the file. Figure 4.25 shows that file 2 can be read or written by process 1, read or appended by process 3, etc. (Actually the access control list is further reduced to a list of User IDs (UIDs) and group IDs (GIDs). A process has the authority assigned to its creating user.)