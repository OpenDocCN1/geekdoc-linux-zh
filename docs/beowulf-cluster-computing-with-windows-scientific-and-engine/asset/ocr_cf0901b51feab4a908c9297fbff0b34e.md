```
int **MPI_File_close**(MPI_File *fh)
```

```
int **MPI_Comm_spawn**(char *command, char *argv\|\|, int maxprocs, MPI_Info info,
                    int root, MPI_Comm comm, MPI_Comm *intercomm,
                    int array_of_errcodes\[\])
```

```
int **MPI_Comm_get_parent**(MPI_Comm *parent)
```

# Fortran routines.

```
**MPI_ISEND**(buf, count, datatype, dest, tag, comm, request, ierror)
<type> buf(*)
integer count, datatype, dest, tag, comm, request, ierror
```

```
**MPI_IRECV**(buf, count, datatype, source, tag, comm, request,ierror)
<type> buf(*)
integer count, datatype, source, tag, comm, request, ierror
```

```
**MPI_WAIT**(request, status, ierror)
integer request,status(MPI_STATUS_SIZE), ierror
```

```
**MPI_TEST**(request, flag, status, ierror)
logical flag
integer request, status(MPI_STATUS_SIZE), ierror
```

```
**MPI_WAITALL**(count, array_of_requests, array_of_statuses,ierror)
integer count, array_of_requests(*),
array_of_statuses(MPI_STATUS_SIZE,*), ierror
```

```
**MPI_WIN_CREATE**(base, size, disp_unit, info, comm, win, ierror)
<type> base(*)
integer(kind=MPI_ADDRESS_KIND) size
integer disp_unit, info, comm, win, ierror
```

```
**MPI_WIN_FREE**(win, ierror)
integer win, ierror
```

```
**MPI_PUT**(origin_addr, origin_count, origin_datatype, target_rank, target_disp,
target_count, target_datatype, win, ierror)
<type> origin_addr(*)
integer(kind=MPI_ADDRESS_KIND) target_disp
```