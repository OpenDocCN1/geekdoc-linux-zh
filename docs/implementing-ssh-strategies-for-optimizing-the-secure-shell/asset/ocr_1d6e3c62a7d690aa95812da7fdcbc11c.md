![](bbox=[0.15, 0.08, 0.68, 0.4])

**Figure 10.9** SFTP settings on the file server’s VShell service.

Next, set the SFTP options for the SFTP subsystem on the file server. The file server’s root-file directory is called Common and is located on a separate 500GB hard drive labeled X, which will be the partition (drive) for the SFTP root directory. Using VShell SFTP will limit all remote-access clients to that directory only and any subdirectories and/or files, as shown in Figure 10.9.

The last order of business is to configure the other clients to use the established SSH connection for communication. While limited space does not allow each step to be described in detail (see Chapter 7 for more detailed steps), the basic idea is to use the loopback interface, 127.0.0.1, for each IP address of the desired server and port, as shown in Table 10.2.

**Table 10.2** Client Specifications

| SERVICE | IP ADDRESS | PORT |
| :--- | :--- | :--- |
| Mail Relay | 127.0.0.1 | 25 |
| Mail Server | 127.0.0.1 | 110 |
| SFTP | 127.0.0.1 | 22 |
| Web (http://127.0.0.1) | 127.0.0.1 | 80 |