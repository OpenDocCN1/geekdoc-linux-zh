certain conditions, the system could deny swap requests because it lacks available data structures, even though the file system has space available for swapping.

“allocate_fs_swapmin” = 1    System allocates sufficient data structures to accommodate the maximum file system swap limit specified by the “swapon(1)” system call or “swapon” command. This ensures that space in memory will support swap requests as long as the file systems have swap space available. This mode is most commonly used on high availability systems where prevention of process failures due to unavailable resources is more important than reduced system efficiency caused by reserving resources before they are needed.

# alwaysdump

“alwaysdump” is a bit-map value that defines which classes of kernel memory pages are to be dumped if a kernel panic occurs.

Acceptable Values:

+   Minimum 0
+   Maximum none
+   Default 0

Specify integer value.

# Description

On large systems, the time required to dump system memory when a kernel panic occurs can be excessive or even prohibitive, depending on how much physical memory is installed in the system. Fast-dump capabilities controlled by the “dontdump” and “alwaysdump” parameters provides a means for restricting kernel dumps to specific types of information:

+   * Unused Physical Memory
+   * Kernel Static Data
+   * Kernel Dynamic Data