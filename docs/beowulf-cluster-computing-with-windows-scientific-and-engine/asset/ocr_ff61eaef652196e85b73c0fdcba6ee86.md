```
pvm_exit();
    return( 0 );
}
```

This example illustrates another useful function: `pvm_spawn()`. The ability to spawn a replacement task is a powerful capability in fault tolerance. It is also a key function in adaptive programs, as we will see in the next section.

```
int numt = pvm_spawn( char *task, char **argv, int flag, 
                       char *node, int ntasks, int *tids )
```

The routine `pvm_spawn()` starts up `ntasks` copies of an executable file `task` on the virtual machine. The PVM virtual machine is assumed to be running on the Beowulf cluster. Here `argv` is a pointer to an array of arguments to `task` with the end of the array specified by NULL. If task takes no arguments then `argv` is NULL. The `flag` argument is used to specify options and is a sum of the following options:

+   * `PvmTaskDefault`: has PVM choose where to spawn processes
+   * `PvmTaskHost`: uses a `where` argument to specify a particular host or cluster node to spawn on
+   * `PvmTaskArch`: uses a `where` argument to specify an architecture class to spawn on
+   * `PvmTaskDebug`: starts up these processes under debugger
+   * `PvmTaskTrace`: uses PVM calls to generate trace data
+   * `PvmMppFront`: starts process on MPP front-end/service node
+   * `PvmHostComp`: starts process on complementary host set

For example, `flag = PvmTaskHost + PvmHostComp` spawns tasks on every node but the specified node (which may be the manager, for instance).

On return, `numt` is set to the number of tasks successfully spawned or an error code if no tasks could be started. If tasks were started, then `pvm_spawn()` returns a vector of the spawned tasks' `tids`. If some tasks could not be started, the corresponding error codes are placed in the last (`ntask - numt`) positions of the vector.

In the example above, `pvm_spawn()` is used by the manager to start all the worker tasks and also is used to replace workers who fail during the computation. This type of fault-tolerant method is useful for applications that run continuously with a steady stream of new work coming in, as was the case in our two initial examples. Both used a variation on the above PVM example code for their solution.