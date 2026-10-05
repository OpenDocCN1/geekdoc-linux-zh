# 110 Chapter 9 • Samba

talk to Linux. The latest version of Samba can be found at http://lake.can-berra.edu.au/pub/samba/samba.html.
Let's quickly go through a small network.

# 9.1 Setting Up a MS Windows Network

This is actually easy, if you have Windows for Workgroups, Windows 95, or Windows NT. There are apparently DOS clients as well. So from here on in, we'll just say "Windows" to relate to all three versions of the OS, and you'll have to do some reading to match what I tell you to your particular version of Windows.

# What You'll Need

First, get the ethernet cards and drivers loaded. Also install your backbone.
The best available networking scheme for the money is 10BaseT, as there are fewer problems that can cause the entire network to go down. But it's more expensive; you have to buy a hub, switch, patch cables, patch panels, run one cable to each machine, and so on. But it is certainly worth the money.

If you want a cheaper ethernet, or you have a very small network, you can get the very affordable 10Base2. This is also known as "thinnet." All you have to be concerned about a 10Base2 network that is both ends are terminated with a 50-ohm resistor. Thinnet has the disadvantage that if one section of cable goes down, the entire network goes down.

You'll need to make sure that each Windows user has an account on the Linux server. Their shell can be non-existent if you like, but the account and a home directory have to exist. If you want, make the shell something like /bin/false. If you want users to be able to change their passwords, set the shell to be /bin/passwd. Also be to add /bin/passwd to the /etc/shells file.

Once you have your network and you Linux box set up, get the software working. Windows will allow you to use the Windows networking option to create a simple network. Be sure to use the same workgroup name across all the machines.

# What's a Workgroup?

A workgroup is something similar to a subnet, but not quite the same. A sub-net breaks up you physically, as you need a router or bridge to get from one subnet to another. A workgroup is a more logical breakdown. For example,