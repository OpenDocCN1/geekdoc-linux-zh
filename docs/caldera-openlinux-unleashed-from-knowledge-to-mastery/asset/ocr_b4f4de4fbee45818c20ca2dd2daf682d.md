+   - Use non-routable (private) addresses for machines on the local network. Drop all packets coming from the Internet destined for (or claiming to come from) non-routable addresses. Use masquerading to allow internal machines to access the Internet.

+   - Have all firewall rules log hits. The log should be done on the firewall machine as well as on a logging host on the internal network.

For the ultimate in firewall security, you could set up a firewall something like this:

+   - Use a machine with no hard drive.

+   - Create a write-protected bootable Linux floppy that contains the kernel and a mini-mal file system.

+   - When the firewall boots from the floppy, it should create a RAM disk and use that as a root partition. Once the system has booted, configured all interfaces and set up the firewall rules, delete the sh, route, and ifconfig binaries. (In fact, delete all system binaries—they are not needed once the system is up and running.) Because the binaries are in a RAM disk, the bootable floppy is unaffected.

The beauty of this setup is that the lack of even sh makes it very difficult for an attacker to take control of the firewall. Even if he does somehow manage to get a shell, the attacker cannot permanently modify the firewall setup (which is on a write-protected floppy).

The mechanics of this kind of firewall setup are a bit involved; a starting point is the “Initial RAMDisk” article in /usr/src/linux/Documentation/initrd.txt. Of course, you need a second machine for testing purposes until you have the setup just right.

# ## A Firewall Is Not a Panacea

A firewall prevents certain packets from the Internet from entering your LAN and certain packets from your LAN from entering the Internet. That is all. If you are running a Web browser with an exploitable buffer overrun from behind your firewall, the firewall cannot prevent a buffer overrun attack. For this reason, you need to practice deep security. Make all of your LAN workstations secure enough that you’d feel confident putting them on the Internet even without a firewall. Then put in a firewall anyway.

Each LAN machine (if it is running Linux) should have its own firewall rules to reject packets from outside machines. For example, no outside machine should attempt to access any UNIX services on internal machines, so all packets not coming from the local network destined for ports below 1024 should be blocked.

In particular, internal machines should not trust the firewall. The firewall will be the first machine compromised by an attacker; internal machines should not allow connections originating from the firewall machine.