Specify integer value or use integer formula expression.

# Description

Each set of semaphores allocated per identifier occupies 1 or more contiguous slots in the sem array. As semaphores are allocated and deallocated, the sem array might become fragmented.

`semmap` dimensions the resource map which shows the free holes in the sem array. An entry in this map is used to point to each set of contiguous unallocated slots; the entry consists of a pointer to the set, plus the size of the set.

If semaphore usage is heavy and a request for a semaphore set cannot be accommodated, the following message appears:

> danger: mfree map overflow

You should then configure a new kernel with a larger value for `semmap`.

Fragmentation of the sem array is reduced if all semaphore identifiers have the same number of semaphores; `semmap` can then be somewhat smaller.

Four is the lower limit: 1 slot is overhead for the map and the second slot is always needed at system initialization to show that the sem array is free.

# semume

Define the maximum number of IPC semaphores that a given process can have undo operations pending on.

Acceptable Values:

Minimum: `1`

Maximum: `SemMNS`

Default: `10`

Specify integer value.

# Description

An !!undo!! is a special, optional, flag in a semaphore operation which causes that operation to be undone if the process which invoked it terminates.