
### C 例程

```c
int MPI_Put(void *origin_addr, int origin_count, MPI_Datatype origin_datatype, int target_rank, MPI_Aint target_disp, int target_count, MPI_Datatype target_datatype, MPI_Win *win)

int MPI_Get(void *origin_addr, int origin_count, MPI_Datatype origin_datatype, int target_rank, MPI_Aint target_disp, int target_count, MPI_Datatype target_datatype, MPI_Win *win)

int MPI_Win_fence(int assert, MPI_Win *win)

int MPI_File_open(MPI_Comm comm, char *filename, int amode, MPI_Info info, MPI_File *fh)

int MPI_File_set_view(MPI_File fh, MPI_Offset disp, MPI_Datatype etype, MPI_Datatype datatype, char *data, MPI_Info info)

int MPI_File_read(MPI_File fh, void *buf, int count, MPI_Datatype datatype, MPI_Status *status)

int MPI_File_write(MPI_File fh, void *buf, int count, MPI_Datatype datatype, MPI_Status *status)

int MPI_File_read_all(MPI_File fh, void *buf, int count, MPI_Datatype datatype, MPI_Status *status)

int MPI_File_write_all(MPI_File fh, void *buf, int count, MPI_Datatype datatype, MPI_Status *status)

int MPI_File_close(MPI_File *fh)

int MPI_Comm_spawn(char *command, char *argv[], int maxprocs, MPI_Info info, int root, MPI_Comm comm, MPI_Comm *intercomm, int array_of_errcodes[])

int MPI_Comm_get_parent(MPI_Comm *parent)
```

### Fortran 例程

```fortran
MPI_ISEND(buf, count, datatype, tag, comm, request, error)

<type> buf(*)

integer count, datatype, dest, tag, comm, request, ierror

MPI_IRECV(buf, count, datatype, source, tag, request, ierror)

<type> buf(*)

integer count, datatype, source, tag, comm, request, ierror

MPI_WAIT(request, status, ierror)

integer request, status(MPI_STATUS_SIZE), ierror

MPI_TEST(request, flag, status, ierror)

logical flag

integer request, status(MPI_STATUS_SIZE), ierror

MPI_WAITALL(count, array_of_requests, array_of_statuses)

integer count, array_of_requests(*), array_of_statuses(MPI_STATUS_SIZE,*), ierror

MPI_WIN_CREATE(base, size, disp_unit, info, comm, win, ierror)

<type> base(*)

integer(kind=MPI_ADDRESS_KIND) size

integer disp_unit, info, comm, win, ierror

MPI_WIN_FREE(win, ierror)

integer win, ierror
```
