
```c
/* check for error */
if (mytid < 0) {
  /* print out the error */
  pvm_perror(argv[0]);
  /* exit the program */
  return -1;
}

/* join the mmult group */
mygid = pvm_joining(mmy);
if (mygid < 0) {
  pvm_perror(argv[0]); pvm_exit(); return -1;
}

/* if my group id is 0 then I must spawn the other tasks */
if (mygid == 0) {
  /* find out how many tasks to spawn */
  if (argc == 3) {
    m = atoi(argv[1]);
    blksz = atoi(argv[2]);
  }
  if (argc < 3) {
    fprintf(stderr, "Usage: mmult m blk\n");
    pvm_lvgroup("mmult"); pvm_exit(); return -1;
  }
  
  /* make sure ntask is legal */
  ntask = m*m;
  if ((ntask < 1) || (ntask >= MAXNTIDS)) {
    fprintf(stderr, "ntask = %d not valid.\n", ntask);
    pvm_lvgroup("mmult"); pvm_exit(); return -1;
  }
  /* no need to spawn if there is only one task */
  if (ntask == 1) goto barrier;

  /* spawn the child tasks */
  info = pvm_spawn("mmult", (char**)0, PvmTaskDefault, (char**)0,
    ntask-1, child);

  /* make sure spawn succeeded */
  if (info != ntask-1) {
    pvm_lvgroup("mmult"); pvm_exit(); return -1;
  }

/* send the matrix dimension */
pvm_initsend(PvmDataDefault);
pvm_pkint(&m, 1, 1);
pvm_pkint(&blksize, 1, 1);
pvm_mcast(child, ntask-1, DMTAG);
} else {
/* recv the matrix dimension */
pvm_recv(pvm_gettid("mmult", 0), DMTAG);
pvm_upkint(&m, 1, 1);
pvm_upkint(&blksize, 1, 1);
task = m*n;
}

/* make sure all tasks have joined the group */
barrier:
info = pvm_barrier("mmult", ntask);
if (info < 0) pvm_perror(argv[0]);

/* find the tids in my row */
for (i = 0; i < m; i++)
myrow[i] = pvm_gettid("mmult", (mygid/m)*m + i);

/* allocate the memory for the local blocks */
a = (float*)malloc(sizeof(float)*blksize*blksize);
b = (float*)malloc(sizeof(float)*blksize*blksize);
c = (float*)malloc(sizeof(float)*blksize*blksize);
atmp = (float*)malloc(sizeof(float)*blksize*blksize);
/* check for valid pointers */
if (!(a && b && c && atmp)) {
fprintf(stderr, "%s: out of memory!\n", argv[0]);
free(a); free(b); free(c); free(atmp);
pvm_lvgroup("mmult"); pvm_exit(); return -1;
}

/* find my block's row and column */
row = mygid/m; col = mygid % m;
/* calculate the neighbor's above and below me */
up = pvm_gettid("mmult", ((row + m - 1) % (m - 1)) * m + col);
down = pvm_gettid("mmult", ((row == (m-1)) ? 0 : (row+1)*m + col));

/* initialize the blocks */
InitBlock(a, b, c, blksize, row, col);

/* do the matrix multiply */
for ( i = 0; i < m; i++) {
/* mcast the block of matrix A */
if (col == (row + i)%m) {
pvm_initsend(PvmDataDefault);
pvm_pkfloat(a, blksize*blksize, 1);
pvm_mcast(myrow, m, (i+1)*ATAG);
BlockMult(c,a,b,blksize);
}
else {
pvm_recv(pvm_gettid("mmult", row*m + (row +i)%m), (i+1)*ATAG);
pvm_upkfloat(atmp, blksize*blksize, 1);
BlockMult(c,atmp,b,blksize);
}
/* rotate the columns of B */
pvm_initsend(PvmDataDefault);
pvm_pkfloat(b, blksize*blksize, 1);
pvm_send(up, (i+1)*FTAG);
pvm_recv(down, (i+1)*FTAG);
pvm_upkfloat(b, blksize*blksize, 1);
}
/* check it */
for ( i = 0 ; i < blksize*blksize; i++)
if (a[i] != c[i])
printf("Error a[%d] (%g) != c[%d] (%g) \n", i, a[i],i,c[i]);
printf("Done.\n");
free(a); free(b); free(c); free(atmp);
pvm_lvgroup("mmult");
pvm_exit();
return 0;
}
```

## 11.6 One-Dimensional Heat Equation

Here we present a PVM program that calculates heat diffusion through a substrate, in this case a wire. Consider the one-dimensional heat equation on a thin wire:

$$\frac{\partial A}{\partial t} = \frac{\partial^{2} A}{\partial x^{2}} \quad (11.6.1)$$

and a discretization of the form

$$\frac{A_{i+1,j}-A_{i,j}}{\triangle t}=\frac{A_{i,j+1}-2A_{i,j}+A_{i,j-1}}{\triangle x^{2}},$$

giving the explicit formula

$$A_{i+1,j}=A_{i,j}+\frac{\triangle t}{\triangle x^{2}}(A_{i,j+1}-2A_{i,j}+A_{i,j-1}).$$

The initial and boundary conditions are

$$A(t,0)=0, A(t,1)=0 \text{ for all } t$$
$$A(0,x)=\sin(\pi x) \text{ for } 0 \leq x \leq 1.$$

The pseudocode for this computation is as follows:

```text
for i = 1: tsteps-1;

t = t+dt;

a(i+1,1)=0;

a(i+1,n+2)=0;

for j = 2:n+1;

a(i+1,j)=a(i,j) + mu*(a(i,j+1)-2*a(i,j)+a(i,j-1));

end

end
```

For this example we use a master/worker programming model. The master, `heat.c`, spawns five copies of the program `heatslv`. The workers compute the heat diffusion for subsections of the wire in parallel. At each time step the workers exchange boundary information, in this case the temperature of the wire at the boundaries between processors.

Let’s take a closer look at the code. In `heat.c` the array `solution` will hold the solution for the heat diffusion equation at each time step. First the `heatslv` tasks are spawned. Next, the initial dataset is computed. Notice the ends of the wires are given initial temperature values of zero.

The main part of the program is then executed four times, each with a different value for $\Delta t$. A timer is used to compute the elapsed time of each compute phase. The initial datasets are sent to the `heatslv` tasks. The left and right neighbor task ids are set along with the initial dataset. The `heatslv` tasks use these to communicate boundary information. Alternatively, we could have used the PVM group calls to map tasks to segments of the wire. By using this approach we would have avoided explicitly communicating the task ids to the slave processes.

After sending the initial data, the master process waits for results. When the results arrive, they are integrated into the solution matrix, the elapsed time is calculated, and the solution is written to the output file.

Once the data for all four phases have been computed and stored, the master program prints out the elapsed times and kills the slave processes.

```c
/*
heat.c

Use PVM to solve a simple heat diffusion differential equation,
using 1 master program and 5 slaves.

The master program sets up the data, communicates it to the slaves
and waits for the results to be sent from the slaves.
Produces xgraph ready files of the results.
*/
#include "pvm3.h"
#include <stdio.h>
#include <math.h>
#include <time.h>
#define SLAVENAME "heatslv"
#define NPROC 5
#define TIMESTEP 100
#define PLOTINC 10
#define SIZE 1000

int num_data = SIZE/NPROC;

main()
{
int mytid, task_ids[NPROC], i, j;
int left, right, k, l;
int step = TIMESTEP;
int info;

double init[SIZE], solution[TIMESTEP] [SIZE];
double result[TIMESTEP*SIZE/NPROC], deltaz2;
FILE *filenum;
char *filenames[4] [7];
double deltaz[4];
time_t t0;
int etime[4];

filename[0][0] = "graph1";
filename[1][0] = "graph2";
filename[2][0] = "graph3";
filename[3][0] = "graph4";

deltat[0] = 5.0e-1;
deltat[1] = 5.0e-3;
deltat[2] = 5.0e-6;
deltat[3] = 5.0e-9;

/* enroll in pvm */
mytid = pvm_mytid();

/* spawn the slave tasks */
info = pvm_spawn(SLAVENAME, (char *)0, PvmTaskDefault, "",
    NPROC, task_ids);

/* create the initial data set */
for (i = 0; i < SIZE; i++)
    init[i] = sin(M_PI * (double)i / (double)(SIZE-1) ));
init[0] = 0.0;
init[SIZE-1] = 0.0;

/* run the problem 4 times for different values of delta t */
for (l = 0; l < 4; l++) {
    deltax2 = (deltat[l]/pow(1.0/(double)SIZE,2.0));
    /* start timing for this run */
    time(&t0);
    etime[l] = t0;

    /* send the initial data to the slaves. */
    /* include neighbor info for exchanging boundary data */
    for (i = 0; i < NPROC; i++) {
        pvm_initsend(PvmDataDefault);
        left = (i == 0) ? 0 : task_ids[i-1];
        pvm_pkint(&left, 1, 1);
        right = (i == (NPROC-1)) ? 0 : task_ids[i+1];
        pvm_pkint(&right, 1, 1);
        pvm_pkdouble(&deltax2, 1, 1);
        pvm_pkint(&num_data, 1, 1);
        pvm_pkdouble(&init[num_data*i], num_data, 1);
        pvm_send(task_ids[i], 4);
    }

    /* wait for the results */
    for (i = 0; i < NPROC; i++) {
        pvm_recv(task_ids[i], 7);
        pvm_upkdouble(&result[0], num_data*TIMESTEP, 1);
    }
    /* update the solution */
    for (j = 0; j < TIMESTEP; j++)
        for (k = 0; k < num_data; k++)
            solution[j][num_data*k+i] = result[i*(j,k)];
    }
    /* stop timing */
    time(&t0);
    etime[l] = t0 - etime[l];
    /* produce the output */
    filenum = fopen(filename[l][0], "w");
    fprintf(filenum,"TitleText: Wire Heat over Delta Time: %f\n", deltat[l]);
    fprintf(filenum,"XUnitText: Distance\nYUnitText: Heat\n");
    for (i = 0; i < TIMESTEP; i = i + PLOTINC) {
        fprintf(filenum,"\"Time index: %d\n",i);
        for (j = 0; j < SIZE; j++)
            fprintf(filenum,"%d %f\n",j, solution[i][j]);
        fprintf(filenum,"\n");
    }
    fclose (filenum);
}
/* print the timing information */
printf("Problem size: %d\n",SIZE);
for (i = 0; i < 4; i++)
    printf("Time for run %d: %d sec\n",i,etime[i]);
/* kill the slave processes */
for (i = 0; i < NPROC; i++)
    pvm_kill(task_ids[i]);
pvm_exit();
}
```

The `heatslv` programs do the actual computation of the heat diffusion through the wire. The worker program consists of an infinite loop that receives an initial
