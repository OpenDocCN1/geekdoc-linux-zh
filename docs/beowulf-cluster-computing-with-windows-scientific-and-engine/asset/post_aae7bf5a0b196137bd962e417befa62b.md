
## 9.4 Collective Operations

A *collective* operation is an MPI function that is called by all processes belonging to a communicator. (If the communicator is `MPI_COMM_WORLD`, this means all processes, but MPI allows collective operations on other sets of processes as well.)

Collective operations involve communication and also sometimes computation, but since they describe particular patterns of communication and computation, the MPI implementation may be able to optimize them beyond what is possible by expressing them in terms of MPI point-to-point operations such as `MPI_Send` and `MPI_Recv`. The patterns are also easier to express with collective operations.

Here we introduce two of the most commonly used collective operations and show how the communication in a parallel program can be expressed entirely in terms of collective operations with no individual `MPI_Sends` or `MPI_Revc`s at all. The program shown in Figure 9.11 computes the value of $\pi$ by numerical integration. Since
$$ \int_0^1 \frac{1}{1+x^2} dx = \arctan(x)|_0^1 = \arctan(1) - \arctan(0) = \arctan(1) = \frac{\pi}{4}, $$
we can compute $\pi$ by integrating the function $f(x) = 4/(1+x^2)$ from 0 to 1. We compute an approximation by dividing the interval [0,1] into some number of subintervals and then computing the total area of these rectangles by having each process compute the areas of some subset. We could do this with a manager/worker algorithm, but here we reassign the work. In fact, each worker can compute its set of tasks, and so the “manager” can be a worker, too, instead of just managing the pool of work. The more rectangles there are, the more work there is to do and the more accurate the resulting approximation of $\pi$ is.

To experiment, let us make the number of subintervals a command-line argument. (Although the MPI standard does not guarantee that any process receives command-line arguments, in most implementations, especially for Beowulf clusters, one can assume that at least the process with rank 0 can use argc and argv, although they may not be meaningful until after MPI_Init is called.) In our example, process 0 sets n, the number of subintervals, to argv[1]. Once a process knows n, it can claim approximately 1/n of the work by claiming every nth rectangle, starting with the one numbered by its own rank. Thus process j computes the areas of rectangles j, j + n, j + 2n, and so on.

Not all MPI implementations make the command-line arguments available to all processes, however, so we start by having process 0 send n to each of the other processes. We could have a simple loop, sending n to each of the other processes one at a time, but this is inefficient. If we know that the same message is to be delivered to all the other processes, we can ask the MPI implementation to do this in a more efficient way than with a series of MPI_Sends and MPI_Recvs.

Broadcast (MPI_Bcast) is an example of an MPI collective operation. A collective operation must be called by all processes in a communicator. This allows an implementation to arrange the communication and computation specified by a collective operation in a special way. In the case of MPI_Bcast, an implementation is likely to use a tree of communication, sometimes called a spanning tree, in which process 0 sends its message to a second process, then both processes send to two more, and so forth. In this way most communication takes place in parallel, and all the messages have been delivered in $\log_2 n$ steps.

The precise semantics of MPI_Bcast is sometimes confusing. The first three arguments specify a message with (address, count, datatype) as usual. The fourth argument (called the root of the broadcast) specifies which of the processes owns the data that is being sent to the other processes. In our case it is process 0. MPI_Bcast acts like an MPI_Send on the root process and like an MPI_Recv on all the other processes, but the call itself looks the same on each process. The last argument is the communicator that the collective call is over. All processes in the communicator must make this same call. Before the call, n is valid only at the root; after MPI_Bcast has returned, all processes have a copy of the value of n.

Next, each process, including process 0, adds up the areas of its rectangles into the local variable mypi. Instead of sending these values to one process and having that process add them up, however, we use another collective operation, `MPI_Reduce`. `MPI_Reduce` performs not only collective communication but also collective computation. In the call
```c
MPI_Reduce( &mypi, &pi, 1, MPI_DOUBLE, MPI_SUM, 0,
            MPI_COMM_WORLD);
```
the sixth argument is again the root. All processes call `MPI_Reduce`, and the root process gets back a result in the second argument. The result comes from performing an arithmetic operation, in this case summation (specified by the fifth argument), on the data items on all processes specified by the first, third, and fourth arguments.

Process 0 concludes by printing out the answer, the difference between this approximation and a previously computed accurate value of $\pi$, and the time it took to compute it. This illustrates the use of `MPI_Wtime`.

`MPI_Wtime` returns a double-precision floating-point number of seconds. This value has no meaning in itself, but the *difference* between two such values is the wall-clock time between the two calls. Note that calls on two different processes are not guaranteed to have any relationship to one another, unless the MPI implementation promises that the clocks on different processes are *synchronized* (see `MPI_WTIME_IS_GLOBAL` in any of the MPI books).

The routine `MPI_Allreduce` computes the same result as `MPI_Reduce` but returns the result to all processes, not just the root process. For example, in the Jacobi iteration, it is common to use the two-norm of the difference between two successive iterations as a measure of the convergence of the solution.

```c
...
norm2local = 0.0;
for (ii=1; ii<i_end-i_start+1; ii++)
  for (jj=1; jj<NY; jj++)
    norm2local += ulocal[ii][jj] * ulocal[ii][jj];
MPI_Allreduce( &norm2local, &norm2, 1, MPI_DOUBLE, MPI_SUM,
               MPI_COMM_WORLD );
norm2 = sqrt( norm2 );
```
Note that `MPI_Allreduce` is not a routine for computing the norm of a vector. It merely combines values contributed from each process in the communicator.

### Figure 9.11

Computing $\pi$ using collective operations.

```c
#include "mpi.h"
#include <stdio.h>
#include <math.h>

double f(double a) { return (4.0 / (1.0 + a*a)); }

int main(int argc, char *argv[])
{
    int n, myid, numprocs, i;
    double PI25DT = 3.141592653589793238462643;
    double mypi, pi, h, sum, x;
    double starttime = 0.0, endtime;

    MPI_Init(&argc, &argv);
    MPI_Comm_size(MPI_COMM_WORLD, &numprocs);
    MPI_Comm_rank(MPI_COMM_WORLD, &myid);

    if (myid == 0) {
        starttime = MPI_Wtime();
        n = atoi(argv[1]);
    }
    MPI_Bcast(&n, 1, MPI_INT, 0, MPI_COMM_WORLD);
    h = 1.0 / (double) n;
    sum = 0.0;

    for (i = myid + 1; i <= n; i += numprocs) {
        x = h * (double)i - 0.5;
        sum += f(x);
    }
    mypi = h * sum;
    MPI_Reduce(&mypi, &pi, 1, MPI_DOUBLE, MPI_SUM, 0, MPI_COMM_WORLD);

    if (myid == 0) {
        endtime = MPI_Wtime();
        printf("pi is approximately %.16f, Error is %.16f\n",
               pi, fabs(pi - PI25DT));
        printf("wall clock time = %f\n", endtime - starttime);
    }
    MPI_Finalize();
    return 0;
}
```

### Figure 9.10

A better version of the neighbor exchange code.

```c
/* Better exchange code. */
void exchange_nbrs( double ulocal[][NY+2], int i_start, int i_end,
                    int left, int right )
{
   MPI_Status status;
   int c;

   /* Send and receive from the left neighbor */
   MPI_Sendrecv( &ulocal[1][1], NY, MPI_DOUBLE, left, 0,
                 &ulocal[0][1], NY, MPI_DOUBLE, left, 0,
                 MPI_COMM_WORLD, &status );

   /* Send and receive from the right neighbor */
   c = i_end - i_start + 1;
   MPI_Sendrecv( &ulocal[c][1], NY, MPI_DOUBLE, right, 0,
                 &ulocal[c+1][1], NY, MPI_DOUBLE, right, 0,
                 MPI_COMM_WORLD, &status );
}
```

### Figure 9.9

A simple version of the neighbor exchange code. See the text for a discussion of the limitations of this routine.

```c
void exchange_nbrs( double ulocal[][NY+2], int i_start, int i_end, int left, int right )
{
  MPI_Status status;
  int c;

  /* Send and receive from the left neighbor */
  MPI_Send( &ulocal[1][i_start], NY, MPI_DOUBLE, left, 0,
            MPI_COMM_WORLD );
  MPI_Recv( &ulocal[0][i_start], NY, MPI_DOUBLE, left, 0,
            MPI_COMM_WORLD, &status );

  /* Send and receive from the right neighbor */
  c = i_end - i_start + 1;
  MPI_Send( &ulocal[c+1][i_start], NY, MPI_DOUBLE, right, 0,
            MPI_COMM_WORLD );
  MPI_Recv( &ulocal[c+1][i_start], NY, MPI_DOUBLE, right, 0,
            MPI_COMM_WORLD, &status );
}
```

operation is ignored. MPI also provides routines to compute the neighbors in a regular mesh of arbitrary dimension and to help an application choose a decomposition that is efficient for the parallel computer.

The code in `exchange_nbrs` will work with most MPI implementations for small values of n but, as described in Section 10.3, is not good practice (and will fail for values of NY greater than an implementation-defined threshold). A better approach in MPI is to use the `MPI_Sendrecv` routine when exchanging data between two processes, as shown in Figure 9.10.

In Sections 10.3 and 10.7, we discuss other implementations of the exchange routine that can provide higher performance. MPI support for more scalable decompositions of the data is described in Section 10.3.2.
