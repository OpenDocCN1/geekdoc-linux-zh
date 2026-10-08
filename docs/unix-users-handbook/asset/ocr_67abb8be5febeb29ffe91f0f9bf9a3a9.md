much easier to maintain naming information, because it only needs to be kept in a few places as opposed to on each system.

Clients use a file called `/etc/resolv.conf` to configure the resolver. The name server and its corresponding address are the keys to resolving information.

This solution makes it much easier to maintain system names and addresses in large environments. DNS and BIND are primarily a system administration exercise to setup. From a user stand-point, you don't need to know much about them. What I will instead focus on in the upcoming sections are some of the programs in which users are more interested. I will supply some background so that the way in which the programs are used has more meaning. In general, though, I'll concentrate on the user aspect of these networking topics, as opposed to the system administration aspect of them.

# /etc/hosts

This file contains information about the other systems to which you are connected. It contains the Internet address of each system, the system name, and any aliases for the system name. If your system administrator modifies your `/etc/hosts` file to contain the names of the systems on your network, they have provided the basis for **rlogin** to another system. Although you can now **rlogin** to other UNIX systems, you cannot yet **rcp** or **remsh** to another system. Although adding **remsh** and **rcp** functionality is easy, it does indeed compromise security, so it is not always set up on all systems. Here is an example `/etc/hosts` file:

127.0.0.1  localhost  loopback
15.32.199.42  a4410827
15.32.199.28  a4410tu8
15.32.199.7  a4410922
15.32.199.21  a4410tu1
15.32.199.22  a4410tu2

![](bbox=[0.88, 0.51, 0.97, 0.6])

![](bbox=[0.88, 0.61, 0.97, 0.7])

![](bbox=[0.88, 0.7, 0.97, 0.79])