
However, this can be awkward to implement, particularly for more complex communication patterns; in addition, it does not address the extra copy that may be performed by `MPI_Send`.

The approach used by MPI, following earlier message-passing systems as well as nonblocking sockets (see [6, Chapter 9]), is to split the send and receive operations into two steps: one to initiate the operation and one to complete the operation. Other operations, including other communication operations, can be issued between the two steps. For example, an MPI receive operation can be initiated by a call to `MPI_Irecv` and completed with a call to `MPI_Wait`. Because the routines that initiate these operations do not wait for them to complete, they are called nonblocking operations. The "I" in the routine name stands for "immediate"; this indicates that the routine may return immediately without completing the operation. The arguments to `MPI_Irecv` are the same as for `MPI_Recv` except for the last (status) argument. This is replaced by an `MPI_Request` value; it is a handle that is used to identify an initiated operation. To complete a nonblocking operation, the request is given to `MPI_Wait`, along with a status argument; the status argument serves the same purpose as status for an `MPI_Recv`. Similarly, the nonblocking counterpart to `MPI_Send` is `MPI_Isend`; this has the same arguments as `MPI_Send` with the addition of an `MPI_Request` as the last argument (in C). Using these routines, our example becomes the following:

```c
if ( rank == 0 ) {
    MPI_Request req1, req2;
    MPI_Isend( sbuf, n, MPI_INT, 1, 0, MPI_COMM_WORLD, &req1 );
    MPI_Irecv( rbuf, n, MPI_INT, 1, 0, MPI_COMM_WORLD, &req2 );
    MPI_Wait( &req1, &status );
    MPI_Wait( &req2, &status );
}
else if ( rank == 1 ) {
    MPI_Request req1, req2;
    MPI_Irecv( rbuf, n, MPI_INT, 0, 0, MPI_COMM_WORLD, &req1 );
    MPI_Isend( sbuf, n, MPI_INT, 0, 0, MPI_COMM_WORLD, &req2 );
    MPI_Wait( &req1, &status );
    MPI_Wait( &req2, &status );
}
```

The buffer *sbuf* provided to `MPI_Isend` must not be modified until the operation is completed with `MPI_Wait`. Similarly, the buffer *rbuf* provided to `MPI_Irecv` must not be modified or read until the `MPI_Irecv` is completed.

The nonblocking communication routines allow the MPI implementation to wait until the message can be sent directly from one user buffer to another (e.g., from *sbuf* to *rbuf*) without requiring any copy or using any system buffer space.

Because it is common to start multiple nonblocking operations, MPI provides routines to test or wait for completion of any one, all, or some of the requests. For example, `MPI_Waitall` waits for all requests in an array of requests to complete. Figure 10.4 shows the use of nonblocking communication routines for the Jacobi example.¹

MPI nonblocking operations are not the same as asynchronous operations. The MPI standard does not require that the data transfers overlap computation with communication. MPI specifies only the semantics of the operations, not the details of the implementation choices. The MPI nonblocking routines are provided primarily for correctness (avoiding the limitations of system buffers) and performance (avoidance of copies).

### 10.3.2 Communicating Noncontiguous Data in MPI

The one-dimensional decomposition used in the Jacobi example (Section 9.3) is simple but does not scale well and can lead to performance problems. We can analyze the performance of the Jacobi following the discussion in Section 9.2. Let the time to communicate $n$ bytes be

$$T_{comm} = s + rn,\tag{10.3}$$

where $s$ is the *latency* and $r$ is the (additional) time to communicate one byte. The time to compute one step of the Jacobi method, using the one-dimensional decomposition in Section 9.3, is

$$\frac{5n}{p} f + 2(s + rn),$$

where $f$ is the time to perform a floating-point operation and $p$ is the number of processes. Note that the cost of communication is independent of the number of processes; eventually, this cost will dominate the calculation. Hence, a better approach is to use a two-dimensional decomposition, as shown in Figure 10.5.

The time for one step of the Jacobi method with a two-dimensional decomposition is just

$$\frac{5n}{p} f + 4 \left(s + r \frac{n}{\sqrt{p}} \right) .$$

This is faster than the one-dimensional decomposition as long as

$$n > \frac{2}{1 - 4/\sqrt{p}} s .$$

(assuming $p \ge 16$). To implement this decomposition, we need to communicate data to four neighbors, as shown in Figure 10.6.

The left and right edges can be sent and received by using the same code as for the one-dimensional case. The top and bottom edges have noncontiguous data. For example, the top edge needs to send the tenth, sixteenth, and twenty-second element. There are four ways to move this data:

1. Each value can be sent separately. Because of the high latency of message passing, this approach is inefficient and normally should not be used.
2. The data can be copied into a temporary buffer using a simple loop, for example,

```c
for (i=0; i<3; i++) {
    tmp[i] = u_local[i][6];
}
MPI_Send( tmp, 3, MPI_DOUBLE, . . . );
```

This is a common approach and, for some systems and MPI implementations, may be the most efficient.

3. MPI provides two routines to pack and unpack a buffer. These routines are `MPI_Pack` and `MPI_Unpack`. A buffer created with these routines should be sent and received with MPI datatype `MPI_PACKED`. We note, however, that these routines are most useful for complex data layouts that change frequently within a program.

4. MPI provides a way to construct new datatypes representing any data layout. These routines can be optimized by the MPI implementation, in principle providing better performance than the user can achieve using a simple loop [16]. In addition, using these datatypes is crucial to achieving high performance with parallel I/O.

MPI provides several routines to create datatypes representing common patterns of memory. These new datatypes are called derived datatypes. For this case, `MPI_Type_vector` is what is needed to create a new MPI datatype representing data values separated by a constant stride. In this case, the stride is $NY*2$, and the number of elements is $i\_end - i\_start + 1$.

```c
MPI_Type_vector( i_end - i_start + 1, 1, NY*2,
                MPI_DOUBLE, &vctype );
MPI_Type_commit( &vctype );
```

The second argument is a *block count* and is the number of the basic datatype items (`MPI_DOUBLE` in this case); this is useful particularly in multicomponent PDE problems. The routine `MPI_Type_commit` must be called to *commit* the MPI datatype;

---
¹On many systems, calling `MPI_Isend` before `MPI_Irecv` will improve performance.

![](img/e2283ffaea56e577ac05056b4bb738fc_238_0.png)

**Figure 10.5**
Domain and $9 \times 9$ computational mesh for approximating the solution to the Poisson problem using a two-dimensional decomposition.

![](img/e2283ffaea56e577ac05056b4bb738fc_239_0.png)

**Figure 10.6**
Locations of mesh points in ulocal for a two-dimensional decomposition.

**Figure 10.4**
Nonblocking exchange code for the Jacobi example.

```c
void exchange_nbrs( double ulocal[][NY+2], int i_start, int i_end,
                    int left, int right )
{
    MPI_Status  statuses[4];
    MPI_Request requests[4];
    int c;
    /* Begin send and receive from the left neighbor */
    MPI_Isend( &ulocal[i_start][1], NY, MPI_DOUBLE, left, 0,
               MPI_COMM_WORLD, &requests[0] );
    MPI_Irecv( &ulocal[0][i_start], NY, MPI_DOUBLE, left, 0,
               MPI_COMM_WORLD, &requests[1] );
    /* Begin send and receive from the right neighbor */
    c = i_end - i_start + 1;
    MPI_Isend( &ulocal[c][i_start], NY, MPI_DOUBLE, right, 0,
               MPI_COMM_WORLD, &requests[2] );
    MPI_Irecv( &ulocal[c+1][i_start], NY, MPI_DOUBLE, right, 0,
               MPI_COMM_WORLD, &requests[3] );
    /* Wait for all communications to complete */
    MPI_Waitall( 4, requests, statuses );
}
```
