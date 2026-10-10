some of the challenges that kernel programmers face and try to develop a basic understanding of a few of the common programmatic solutions they employ.

# Static Lists (Static Tables)

The kernel often needs to maintain an extensive list of parameters related to some data structure or managed resource. The simplest way to store this type of data is to create an ordered, static list of the attributes of each member of the list.

Each data structure is defined according to the individual pieces of data assigned to each element. Once each parameter is typed, the size (in bytes) of the structure is known. These structures are then stored in contiguous kernel space (as an array of structures) and may be easily indexed for fast access.

As a general observation, and by no means a hard and fast rule, the naming convention of these lists may resemble the following pattern (see Figure 3-3). If the name of the data structure for a single member of the list is defined as data_t, then the kernel pointer to the start of the list would be data*. The list could also be referenced by an array named data [x], and the number of elements would be stored in ndata. Many examples in the kernel follow this convention, but by no means all of them.

# Pros

The space needed for a static list must be allocated during system initialization and is often controlled by a *kernel-tunable parameter*, which is set prior to the building of the kernel image. The first entry in a static data table has the index value of 0, which facilitates easy calculation of the starting address of each element within the table (assuming a fixed size for each member element).

# Example

Assume that each data structure contains exactly 64 bytes of data and that the beginning of the static list is defined by the kernel symbol mylist. If you wanted to access the data for the list member with an index number of 14, you could simply take the address stored in the kernel pointer mylist* and add 14×64 to it to arrive at the byte address corresponding to the beginning of the 15th element in the list (don’t forget that the list index starts with 0). If the structure is defined as an array, you could simplify the access by referencing mylist [14] in your code.

# Cons

The main drawback to this approach is that the kernel must provide enough list elements for all potential scenarios that it may encounter. Many system administrators are considered godlike, but very few are truly clairvoyant! In the case of a static list, the only way for it to grow is for the kernel to be rebuilt and the system rebooted.