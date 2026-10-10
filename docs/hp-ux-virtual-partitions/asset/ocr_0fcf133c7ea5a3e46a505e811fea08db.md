mat. as in the `/etc/hosts` file. Here is the **ifconfig** command I issued to configure the interface:

```
$ /etc/ifconfig lan0 inet 128.185.61.2 netmask 255.255.0.0
```

+   * The `255.255.0.0` corresponds to the hex *ffff*0000* shown earlier for the class “B” subnet mask.

+   * *lan0* is the interface being configured.

+   * *inet* is the address family, which is currently the only one supported for this system.

+   * *128.185.61.2* is the address of the LAN interface for system 1.

+   * **netmask** shows how to subdivide the network.

+   * *255.255.0.0* is the same as *ffff*0000*, which is the netmask for a class “B” address.

I have made good use of **netstat**, **ping**, and **ifconfig** to help get the status of the network. **ifconfig**, **route**, and `/etc/hosts` are used to configure the network, should you identify any changes you need to make. The subnet examples show how flexible you can be when configuring your network for both your current and future needs. In simple networks, you may not need to use many of these commands or complex subnetting. In complex networks, or at times when you encounter configuration difficulties, you may have to make extensive use of these commands. In either case, network planning is an important part of setting up UNIX systems.

Most of the commands used throughout this chapter are a part of every system administrator’s tool box. Networking is so vital to the use of UNIX systems, however, that having background in this area can help with your overall understanding of the system and how to use it more effectively.

# rpingo

As a user, you may have a need to NFS mount a directory on another system or perform some other function that you haven’t before used on your system. You can determine whether various pieces of functionality have been