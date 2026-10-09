double precision MPI_WTIME()

**MPI_SEND**(buf, count, datatype, dest, tag, comm, ierror)  
`<type>` buf\(*)  
integer count, datatype, dest, tag, comm, ierror

**MPI_RECV**(buf, count, datatype, source, tag, comm, status, ierror)  
`<type>` buf\(*)  
integer count, datatype, source, tag, comm,  
status(MPI_STATUS_SIZE), ierror

**MPI_PROBE**(source, tag, comm, status, ierror)  
logical flag  
integer source, tag, comm, status(MPI_STATUS_SIZE), ierror

**MPI_SENDRECV**(sendbuf, sendcount, sendtype, dest, sendtag, recvbuf, recvcount,  
recvtype, recvtag, comm, status, ierror)  
`<type>` sendbuf\(*), recvbuf\(*)  
integer sendcount, sendtype, dest, sendtag, recvcount, recvtype,  
source, recvtag, comm, status(MPI_STATUS_SIZE), ierror

**MPI_ALLREDUCE**(sendbuf, recvbuf, count, datatype, op, comm, ierror)  
`<type>` sendbuf\(*), recvbuf\(*)  
integer count, datatype, op, comm, ierror

C++ routines

void **MPI::Init**(int& argc, char\*\*& argv)

void **MPI::Init**()

int **MPI::Comm::Get_rank**() const

int **MPI::Comm::Get_size**() const

void **MPI::Intracom::Bcast**(void* buffer, int count, const Datatype& datatype,  
int root) const

void **MPI::Intracom::Reduce**(const void* sendbuf, void* recvbuf, int count,  
const Datatype& datatype, const Op& op, int root) const

void **MPI::Finalize**()

double **MPI::Wtime**()