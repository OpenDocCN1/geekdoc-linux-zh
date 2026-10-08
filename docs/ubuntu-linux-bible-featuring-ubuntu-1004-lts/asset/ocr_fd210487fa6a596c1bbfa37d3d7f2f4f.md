if your primary reason for running a virtual machine is to enable you to occasionally run proprietary software (some Microsoft Office component, e.g.), the lack of inbound connections doesn't matter, KVM/QEMU's User Networking is probably all you need. User Networking is active by default, but you can explicitly specify it at the command line by using -net nic -net user command-line options.

The User Networking support provided by KVM/QEMU prevent inbound communication to your virtual machines; it doesn't provide full support for it. KVM and QEMU provide two methods for extending the connectivity of your virtual machines when Using Networking:

+   - redir protocol:host-port:guest-ip:guest-port: Enables you to re-direct incoming connections from a port on the host system to a port on a virtual machine. protocol is one of tcp or udp, host-port is the network port on the host system that should be directed to guest-port on a virtual machine, and guest-ip is the address of the virtual machine if it is not the default value (10.0.2), that is assigned by the internal KVM/QEMU DHCP server. This option and associated value must be provided on the command line when you start the virtual machine. You can specify the-redir option multiple times on the command line to re-direct multiple ports to the virtual machine.
- smb /full/path/to/directory: Uses an internal KVM/QEMU SMB server to export the shared directory as a shared qemu, which the virtual machine can then mount as \GATEWAY-IP\qemu. GATEWAY-IP is the IP address of the network-re-direct inside KVM/QEMU, and is 10.0.2. 2 for Windows XP and Vista virtual machines, although it may differ for other versions of Windows.

While the redir option always works, I have had problems getting the smb option with different versions of KVM and QEMU. A much simpler solution is to run Samba on your Ubuntu host and then configure a shared name qemu in /etc/samba/smb.conf file that looks something like the following:

```
[qemu]
comment = Windows File Share for KVM/QEMU
path = /full/path/to/directory
browseable = yes
read-only = no
public = yes
```

After restarting Samba, you will be able to mount the qemu share as \GATEWAY-IP\qemu from the virtual machine. I have had problems accessing other shares in the host environment from virtual machines, but this approach has always worked for me.