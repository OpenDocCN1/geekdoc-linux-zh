# ## 15—
Pipes and FIFOs

This is the first of four chapters covering Linux's assortment of methods for *interprocess communication*, or IPC. IPC is a generic term referring to the methods that processes use to communicate with each other. Without IPC, processes can exchange data or other information with each other only through the filesystem or—in the case of processes having a common ancestor (such as the parent/child relationship after a `fork`)—through any inherited file descriptors. This chapter discusses pipes and FIFOs, the oldest forms of IPC that UNIX and UNIX-like systems have. The topics covered include the following:

+   - Unnamed pipes
+   
+   • Opening and closing unnamed pipes
+   
+   • Reading and writing unnamed pipes
+   
+   • Using `popen` and `pclose`
+   
+   • Understanding FIFOs
+   
+   • Creating, opening, and closing FIFOs
+   
+   • Reading and writing FIFOs

> • Inheriting file descriptors is discussed in "Using fork", page 78.