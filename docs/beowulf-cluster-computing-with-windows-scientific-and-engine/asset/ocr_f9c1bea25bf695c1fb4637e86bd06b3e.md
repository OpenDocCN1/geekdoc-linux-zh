```
#include "mpi.h"

int main( int argc, char *argv[] )
{
    int numpucs, myrank;
    double b [SIZE], c [SIZE];
    int i, row, myrank;
    double dotp;
    MPI_Status status;
    MPI_Comm parentcomm;

    MPI_Init(&argc,&argv );
    MPI_Comm_size( MPI_COMM_WORLD, &numpus );
    MPI_Comm_rank( MPI_COMM_WORLD, &myrank );

    MPI_Comm_get_Parentp &parentcomm );

    MPI_Bcast( b, SIZE, MPI_DOUBLE, 0, parentcomm );
    ...
    /* same as worker code from original matrix-vector multiply */
    ...

    MPI_Comm_free(parentcomm );
    MPI_Finalize( );
    return 0;
}
```

# Figure 10.2
Dynamic process matrix-vector multiply program, worker part.

use it for communications with that worker rather than use a communicator that contains all of the workers. If an implementation returns "invalid communicator" from an MPI_Send or MPI_Recv call, then the manager has lost contact only with one worker and can still communicate with the other workers through the other, still-intact communicators. Since the manager will be using separate communicators rather than separate ranks in a larger communicator to send and receive messages from the workers, it might be convenient to maintain an array of communicators and a parallel array to remember which row has been last sent to a worker, so that if that worker disappears, the same row can be assigned to a different worker.