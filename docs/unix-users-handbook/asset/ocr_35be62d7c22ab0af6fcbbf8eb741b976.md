+   - **inet** is the address family, which is currently the only one supported for this system.

+   - **128.185.61.2** is the address of the LAN interface for system1.

+   - **netmask** shows how to subdivide the network.

+   - **255.255.0.0** is the same as ffff0000, which is the netmask for a class “B” address.

![](bbox=[0.03, 0.26, 0.12, 0.34])

I have made good use of **netstat**, **ping**, and **ifconfig** to help get the status of the network. **ifconfig**, **route**, and /etc/hosts are used to configure the network, should you identify changes you need to make. The subnet examples show how flexible you can be when configuring your network for both your current and future needs. In simple networks, you may not need to use many of these commands or complex subnetting. In complex networks, or at times when you encounter configuration difficulties, you may have to make extensive use of these commands. In either case, network planning is an important part of setting up UNIX systems.

![](bbox=[0.03, 0.35, 0.12, 0.43])

![](bbox=[0.03, 0.44, 0.12, 0.52])

Most of the commands used throughout this chapter are more a part of your system administrator’s toolbox than they are of your toolbox. Networking is so vital to the use of UNIX systems, however, that having background in this area can help with your overall understanding of the system and how to use it more effectively.

![](bbox=[0.03, 0.53, 0.12, 0.61])

# *rpcinfo*

![](bbox=[0.03, 0.67, 0.12, 0.75])

As a user, you may have a need to NFS mount a directory on another system or perform some other function that you haven’t before used on your system. You can determine whether indeed your system administrator has enabled some functionality that you need by evaluating the daemons running on your system. **rpcinfo** allows you to generate a Remote Procedure Call (RPC) on a system, including your local system, by issuing the command `rpc -p system_name`.

![](bbox=[0.03, 0.76, 0.12, 0.84])

The following example shows issuing `rpcinfo -p` on our local system: