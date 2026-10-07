# Process Structures

is 8 Mbytes, hard limit is 2 Gbytes in Solaris 2.6. In Solaris 2.7, the hard limit is infinite on UltraSPARC-based systems, 2 Gbytes on all others.

+   - CORE — Maximum core file size. Soft and hard limit is infinite. A value of 0 here prevents the creation of a core file.
- NOFILE — Maximum number of open files. Default soft limit is 64, hard limit is 1024.
- VMEM — Maximum address space. Infinite soft and hard limit. In reality, 4 Gbytes is the maximum virtual address space attainable on all Solaris releases up to and including Solaris 2.6. Solaris 7 provides a 64-bit address space when booted as a 64-bit kernel, the Sun UltraSPARC-I and UltraSPARC-II 64-bit processors implement a 44-bit virtual address, allowing for a maximum virtual address space of 16 terabytes.

The uarea where open file information is maintained

Solaris 7 adds a pointer to the uf_entry structure: uf_fpollinfo, which is a pointer to an fpollinfo structure. Solaris 7 also adds new functionality in the form of a poll cache to enhance support of the poll(2) system call. The kernel uses the poll cache to track process file descriptors that are being polled. The fpollinfo structure supports the poll cache implementation.

The following are the uarea support management of the process's open file table:

+   - u_ flock — A kernel mutex to synchronize access to the process open file list.
- u_nof — Number of open file slots (i.e., number of open files in the process).
- u_flist — Pointer to the first uf_entry structure. Structure storage is implemented as an array, indexed by the fd (file descriptor) number.