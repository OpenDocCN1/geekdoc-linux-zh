![](bbox=[0.25, 0.11, 0.81, 0.62])

*Figure 18-2 SFU Authentication*

Authentication requires us to add some basic information about our connection to the NFS server. The User Name and Password are those we use to connect to the NFS Server. These should be set up on the server in advance of attempting to make a connection to the server. You also have the option to use NIS, which won't be part of this example. The server to which you are making an NFS connection must be running the PC NFS daemon. You can check to see whether your server is running this daemon. Figure 18-3 shows checking for pcnfsd on the NFS server: