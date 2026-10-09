```
int MPI::Status::Get_source() const
```

```
int MPI::Status::Get_tag() const
```

```
void MPI::Comm::Recv(void* buf, int count, const Datatype& datatype,
    int source, int tag, Status& status) const
```

```
void MPI::Comm::Recv(void* buf, int count, const Datatype& datatype,
    int source, int tag) const
```

```
void MPI::Comm::Send(const void* buf, int count, const Datatype& datatype,
    int dest, int tag) const
```

```
void MPI::Comm::Probe(int source,int tag, Status& status) const
```

```
void MPI::Comm::Sendrecv(const void *sendbuf, int sendcount,
    const Datatype& sendtype, int dest, int sendtag, void *recvbuf,
    int recvcount, const Datatype& recvtype, int source, int recvtag,
    Status& status) const
```

```
void MPI::IntraComm::Allreduce(const void* sendbuf, void* recvbuf, int count,
    const Datatype& datatype, const Op& op) const
```