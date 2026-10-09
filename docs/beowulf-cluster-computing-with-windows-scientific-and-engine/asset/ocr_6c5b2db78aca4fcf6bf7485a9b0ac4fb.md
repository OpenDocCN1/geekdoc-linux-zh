```
int MPI.Reduce(void *sendbuf, void *recvbuf, int count, MPI_Datatype datatype,
MPI_Op op, int root, MPI_Comm comm)
```

```
int MPI.Finalize()
double MPI.Wtime()
```

```
int MPI.Send(void *buf, int count, MPI_Datatype datatype, int dest, int tag, MPI_Comm comm)
```

```
int MPI.Recv(void *buf, int count, MPI_Datatype datatype, int source, int tag, MPI_Comm comm, MPI_Status *status)
```

```
int MPI.Probe(int source, int tag, MPI_Comm comm, MPI_Status *status)
```

```
int MPI.Sendrecv(void *sendbuf, int sendcount, MPI_Datatype sendtype, int dest, int sendtag, void *recvbuf, int recvcount, MPI_Datatype recvtype, int source, MPI_Datatype recvtag, MPI_Comm comm, MPI_Status *status)
```

```
int MPI.Allreduce(void *sendbuf, void *recvbuf, int count, MPI_Datatype datatype, MPI_Op op, MPI_Comm comm)
```

Fortran routines.

```
MPI.INIT(ierorr)
integer ierror
```

```
MPI.COMM.SIZE(comm, size, ierror)
integer comm, size, ierror
```

```
MPI.COMM.RANK(comm, rank, ierror)
integer comm, rank, ierror
```

```
MPI.BCAST(buffer, count, datatype, root, comm, ierror)
<type> buffer(*)
integer count, datatype, root, comm, ierror
```

```
MPI.REDUCE(sendbuf, recvbuf, count, datatype, op, root, comm, ierror)
<type> sendbuf(*), recvbuf(*)
integer count, datatype, op, root, comm, ierror
```

```
MPI.FINALIZE(ierorr)
integer ierror
```