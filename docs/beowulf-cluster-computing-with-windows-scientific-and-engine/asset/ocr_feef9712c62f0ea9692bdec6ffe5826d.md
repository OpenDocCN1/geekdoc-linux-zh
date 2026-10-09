| C<br>MPI type | Fortran<br>MPI type |
| --- | --- |
| int | MPI_INT | INTEGER | MPI_INTEGER |
| double | MPI_DOUBLE | DOUBLE PRECISION | MPI_DOUBLE_PRECISION |
| float | MPI_FLOAT | REAL | MPI_REAL |
| long | MPI_LONG |  |  |
| char | MPI_CHAR | CHARACTER | MPI_CHARACTER |
|  |  | LOGICAL | MPI_LOGICAL |
| — | MPI_BYTE | — | MPI_BYTE |

Table 9.1 The most common MPI datatypes. C and Fortran types on the same row are often but not always the same type. The type MPI_BYTE is used for raw data bytes and does not coorespond to any particular datatype. The C++ MPI datatypes have the same name as the C datatype, but without the MPI_ prefix, for example, MPI::INT.

# Describing the Destination or Source.

The destination or source is specified by using the rank of the process. MPI generalizes the notion of destination and source rank by making the rank relative to a group of processes. This group may be a subset of the original group of processes. Allowing subsets of processes and using relative ranks make it easier to use MPI to write component-oriented software (more on this in Section 10.4). The MPI object that defines a group of processes (and a special communication context that will be discussed in Section 10.4) is called a communicator. Thus, sources and destinations are given by two parameters: a rank and a communicator. The communicator MPI_COMM_WORLD is predefined and contains all of the processes started by mpirun or mpiexec. As a source, the special value MPI_ANY_SOURCE may be used to indicate that the message may be received from any rank of the MPI processes in this MPI program.

# Selecting among Messages.

The “extra” argument for MPI_Send is a non-negative integer tag value. This tag allows a program to send one extra number with the data. MPI_Recv can use this value either to select which message to receive (by specifying a specific tag value) or to use the tag to convey extra data (by specifying the wild card value MPI_ANY_TAG). In the latter case, the tag value of the received message is stored in the status argument (this is the last parameter to MPI_Recv in the C binding). This is a structure in C, an integer array in Fortran, and a class in C++ . The tag and rank of the sending process can be accessed by referring to the appropriate element of status as shown in Table 9.2.