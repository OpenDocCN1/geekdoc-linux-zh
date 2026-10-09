
sary data conversions. If you are sure no data conversion will be needed since the destination machine uses the same data format, then you can use PvmDataRaw as a parameter to pvm_initSEND(). The pvm_pkint() call places a single integer, mytid, into the message buffer. It is important to make sure the corresponding unpack call exactly matches the pack call. Packing an integer and unpacking it as a float will not work correctly. There should be a one-to-one correspondence between pack and unpack calls. Finally, the message is sent to the parent task using a message tag of JOINTAG.

```c
/*
    Fork Join Example
    Demonstrates how to spawn processes and exchange messages
*/

/* defines and prototypes for the PVM library */
#include <pvm3.h>

/* Maximum number of children this program will spawn */
#define MAXNCHILD   20
/* Tag to use for the join message */
#define JOINTAG     11

int
main(int argc, char* argv[])
{

    /* number of tasks to spawn, use 3 as the default */
    int ntask = 3;
    /* return code from pvm calls */
    int info;
    /* my task id */
    int mytid;
    /* my parent's task id */
    int myparent;
    /* children task id array */
    int child[MAXNCHILD];
    int i, mydata, buf, len, tag, tid;

    /* find out my task id number */
    mytid = pvm_mytid();

    /* check for error */
    if (mytid < 0) {
        /* print out the error */
        pvm_perror (argv [0]);
        /* exit the program */
        return -1;
    }
    /* find my parent’s task id number */
    myparent = pvm_parent ();

    /* exit if there is some error other than PvmNoParent */
    if ((myparent < 0) && (myparent != PvmNoParent)
    && (myparent != PvmParentNotSet)) {
        pvm_perror (argv [0]);
        pvm_exit ();
        return -1;
    }

    /* if i don’t have a parent then i am the parent */
    if (myparent == PvmNoParent || myparent == PvmParentNotSet) {
        /* find out how many tasks to spawn */
        if (argc == 2) ntask = atoi (argv [1]);

        /* make sure ntask is legal */
        if ((ntask < 1) || (ntask > MAXNCHILD)) {
            pvm_exit ();
            return 0;
        }

        /* spawn the child tasks */
        info = pvm_spawn (argv [0], (char ** ) 0, PvmTaskDefault, (char *) 0,
            ntask, child);
        /* print out the task ids */
        for (i = 0; i < ntask; i++)
            if (child[i] < 0)
                /* print the error code in decimal */
                printf("%d", child[i]);
            else
                /* print the task id in hex */
                printf("%lx", child[i]);
        putchar('\n');

        /* make sure spawn succeeded */
        if (info == 0) {
            pvm_exit ();
            return -1;
        }

        /* only expect responses from those spawned correctly */
        ntask = info;

        for (i = 0; i < ntask; i++) {
            /* recv a message from any child process */
            buf = pvm_recv (-1, JOINTAG);
            if (buf < 0)
                pvm_perror ("calling recv");
            info = pvm_bufinfo(buf, &len, &tag, &tid);
            if (info < 0)
                pvm_perror("calling pvm_bufinfo");
            info = pvm_upkint(&mydata, 1, 1);
            if (info < 0)
                pvm_perror("calling pvm_upkint");
            if (mydata != tid)
                printf("This should not happen!\n");
            printf("Length %d, Tag %d, Tid 0x%x\n", len, tag, tid);
        }

        pvm_exit();
        return 0;
    }

    /* i'm a child */
    info = pvm_initsend(PvmDataDefault);
    if (info < 0) {
        pvm_perror("calling pvm_initsend");
        pvm_exit();
        return -1;
    }
    info = pvm_pkint(&mytid, 1, 1);
    if (info < 0) {
        pvm_perror("calling pvm_pkint");
        pvm_exit();
        return -1;
    }
    info = pvm_send(myparent, JOIN_TAG);
    if (info < 0) {
        pvm_perror("calling pvm_send");
        pvm_exit();
        return -1;
    }
    pvm_exit();
    return 0;
}
```

Figure 11.3 shows the output of running fork/join. Notice that the order the messages were received is nondeterministic. Since the main loop of the parent processes messages on a first-come first-served basis, the order of the prints are determined simply by the time it takes messages to travel from the child tasks to the parent.

## 11.4 Dot Product

Here we show a simple Fortran program, PSDOT, for computing a dot product. The program computes the dot product of two arrays, X and Y. First PSDOT calls PVMTIMYID() and PVMFSPARENT(). The PVMFSPARENT call will return PVMNOPARENT if the task wasn't spawned by another PVM task. If this is the case, then PSDOT task is the master and must spawn the other worker copies of PSDOT. PSDOT then asks the user for the number of processes to use and the length of vectors to compute.

```
% forkjoin
t10001c t40149 tc0037
Length 4, Tag 11, Tid t40149
Length 4, Tag 11, Tid tc0037
Length 4, Tag 11, Tid t10001c
% forkjoin 4
t10001e t10001d t4014b tc0038
Length 4, Tag 11, Tid t4014b
Length 4, Tag 11, Tid tc0038
Length 4, Tag 11, Tid t10001d
Length 4, Tag 11, Tid t10001e
```

Figure 11.3
Output of fork/join program.

Each spawned process will receive $n/nproc$ elements of $X$ and $Y$, where $n$ is the length of the vectors and $nproc$ is the number of processes being used in the computation. If $nproc$ does not divide $n$ evenly, then the master will compute the dot product on extra the elements. The subroutine SGENMAT randomly generates values for $X$ and $Y$. PSDOT then spawns $nproc - 1$ copies of itself and sends each new task a part of the $X$ and $Y$ arrays. The message contains the length of the subarrays in the message and the subarrays themselves. After the master spawns the worker processes and sends out the subvectors, the master then computes the dot-product on its portion of $X$ and $Y$. The master process then receives the other local dot products from the worker processes. Notice that the PVMFREECV call uses a wild card $(-1)$ for the task id parameter. This indicates that a message from any task will satisfy the receive. Using the wild card in this manner results in a race condition. In this case the race condition does not cause a problem since addition is commutative. In other words, it doesn't matter in which order we add up the partial sums from the workers. Unless one is certain that the race will not affect the program adversely, race conditions should be avoided.

Once the master receives all the local dot products and sums them into a global dot product, it then calculates the entire dot product locally. These two results are then subtracted and the difference between the two values is printed. A small difference can be expected due to the variation in floating-point roundoff errors.

If the PSDOT program is a worker, then it receives a message from the master process containing subarrays of $X$ and $Y$. It calculates the dot product of these subarrays and sends the result back to the master process. In the interests of brevity we do not include the SGENMAT and SDOT subroutines.

```fortran
      PROGRAM PSDOT

* PSDOT performs a parallel inner (or dot) product, where the vectors
* X and Y start out on a master node, which then sets up the virtual
* machine, farms out the data and work, and sums up the local pieces
* to get a global inner product.
*
*   .. External Subroutines ..
*   EXTERNAL PVMFYTID, PVMFSPARENT, PVMFSPAWN, PVMFEXIT, PVMFINIT,SEND
*   EXTERNAL PVMFPACK, PVMFSEND, PVMFRECV, PVMFUNPACK, SGENMAT
*
*   .. External Functions ..
*   INTEGER ISAMAX
*   REAL SDOT
*   EXTERNAL ISAMAX, SDOT
*
*   .. Intrinsic Functions ..
*   INTRINSIC MOD
*
*   .. Parameters ..
*   INTEGER MAXN
*   PARAMETER ( MAXN = 8000 )
*   INCLUDE 'fpvm3.h'
*
*   .. Scalars ..
*   INTEGER N, LN, MYTID, NPROCS, IBUF, IERR
*   INTEGER I, J, K
*   REAL LDOT, GDOT
*
*   .. Arrays ..
*   INTEGER TIDS(0:63)
*   REAL X(MAXN), Y(MAXN)
*
*   Enroll in PVM and get my and the master process' task ID number
*
*   CALL PVMFYTID( MYTID )
*   CALL PVMFSPARENT( TIDS(0) )
*
*   If I need to spawn other processes ( I am master process)
*
*   IF ( TIDS(0) .EQ. PVMOPARENT ) THEN
*
*       Get starting information

      WRITE( *,* ) 'How many processes should participate (1-64)?'
      READ(*,*) NPROCS
      WRITE(*,2000) MAXN
      READ(*,*) N
      TIDS(0) = MYTID
      IF ( N .GT. MAXN ) THEN
        WRITE(*,*) 'N too large. Increase parameter MAXN to run'///
      'this case.'
        STOP
      END IF
*
*   LN is the number of elements of the dot product to do locally. Everyone has the same number, with the master getting any left over elements. J stores the number of elements rest of procs do.

      J = N / NPROCS
      LN = J + MOD(N, NPROCS)
      I = LN + 1
*
*   Randomly generate X and Y
*   Note: SGENMAT() routine is not provided here

      CALL SGEMAT( N, 1, X, N, MYTID, NPROCS, MAXN, J )
      CALL SGEMAT( N, 1, Y, N, I, N, LN, NPROCS )
*
*   Loop over all worker processes

      DO 10 K = 1, NPROCS-1
*
*   Spawn process and check for error

        CALL PVMFSPAWN( 'psdot', 0, 'anywhere', 1, TIDS(K), IERR )
        IF ( IERR .NE. 1 ) THEN
          WRITE(*,*) 'ERROR, could not spawn process #',K,
     :' Dying . . .'
          CALL PVMFEXIT( IERR )
          STOP
        END IF
*
*   Send out startup info

        CALL PVMFINITSEND( PVMDEFAULT, IBUF )
        CALL PVMFPACK( INTEGER4, J, J, 1, 1, IERR )
```
