# ## Server Processes

When a user connects into the Oracle Database server, a server process (sometimes known as shadow process) is created on behalf of the user. The server processes communicate with the user and interact with Oracle to carry out the user’s requests. For example, if the user process requests a piece of data not already in the SGA, the shadow process is responsible for reading the data blocks from the datafiles into the SGA. There can be a one-to-one correlation between the user processes and the shadow processes (as in a dedicated server configuration). Although one shadow process can connect to multiple user processes (as in a multithreaded server configuration), doing so reduces the utilization of system resources.

# ## PGA Memory

The PGA is a memory area that contains data and control information for the Oracle server processes. The amount and content of the PGA depends on the Oracle server options you have installed. This area is made up of the following components:

+   *   **Stack space** This is the memory that holds the session’s variables, arrays, and so on.

+   *   **Session information** If you are not running the multithreaded server, the session information is stored in the PGA. If you are running the multithreaded server, the session information is stored in the SGA.

+   *   **Private SQL area** This is an area in the PGA where information such as binding variables and runtime buffers are kept.

It is important to keep the user’s memory in mind when you are sizing your system, since there might be hundreds of users simultaneously connected to the Oracle Database server. It is the sum of the memory of all of these users that will add up to the total memory used by the user processes. Later in this book, you will see how to configure the memory for both the SGA and PGA memory areas.

# ## MTS vs. Dedicated Server Processes

With a dedicated server process, there is a one-to-one correlation between the user process and the server process. Each server process is dedicated to one user process. With large systems, you could potentially have huge numbers of users connected into the Oracle Database server, and thus huge numbers of processes. In order to reduce the number of processes, you can use some sort of transaction monitor or multiplexer, or you can use the Oracle multithreaded server option. MTS allows multiple user connections to share the same server processes.