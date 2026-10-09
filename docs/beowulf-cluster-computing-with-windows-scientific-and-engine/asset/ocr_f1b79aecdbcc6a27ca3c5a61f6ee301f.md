# **12.3 Adaptive Programs**

In this section, we use some more of the PVM virtual machine functions to illustrate how cluster programs can be extended to adapt not only to faults but also to many other metrics and circumstances. The first example demonstrates a parallel application that dynamically adapts the size of the virtual machine through adding and releasing nodes based on the computational needs of the application. Such a feature is used every day on a 128-processor Beowulf cluster at Oak Ridge National Laboratory that is shared by three research groups.

```
```
int numh = pvm_addhosts( char **hosts, int nhost, int *infos)
int numh = pvm_delhosts( char **hosts, int nhost, int *infos)
```
```

The PVM addhosts and delhosts routines add or delete a set of hosts in the virtual machine. In a Beowulf cluster this corresponds to adding or deleting nodes from the computation; **numh** is returned as the number of nodes successfully added or deleted. The argument **infos** is an array of length **nhost** that contains the status code for each individual node being added or deleted. This allows you to check whether only one of a set of hosts caused a problem, rather than trying to add or delete the entire set of hosts again.

```
```
/*
 * Adaptive Host Allocation Example adds and removes cluster nodes
 * from computation on the fly for different computational phases
 */

#include <stdio.h>
#include <pvm3.h>

static char *host_set_A[] = { "msr", "nova", "sun4" };
static int nhosts_A = sizeof( host_set_A ) / sizeof( char ** );
static char *host_set_B[] = { "davinci", "nimbus" };
static int nhosts_B = sizeof( host_set_B ) / sizeof( char ** );

#define MAX_HOSTS   255
#define MSGTAG      123

double phase1( int prob ) {
    return( (prob == 1) ? 1 : ((double) prob * phase1( prob - 1 )) ); }

double phase2( int prob ) {
```
```