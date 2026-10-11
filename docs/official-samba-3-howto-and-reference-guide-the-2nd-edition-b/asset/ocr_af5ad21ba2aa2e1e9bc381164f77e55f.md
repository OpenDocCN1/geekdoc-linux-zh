I even got sound playing from the Remote X app to my local boxes, and had a working “copy” “paste” from an NX window (running a KDE session in Italy) to my Mozilla mailing agent. These guys are certainly doing something right!

I recommend test driving NX to anybody with a only a passing interest in remote computing the NX⁴ utility.

Just download the free-of-charge client software (available for Red Hat, SuSE, Debian and Windows) and be up and running within 5 minutes (they need to send you your account data, though, because you are assigned a real UNIX account on their testdrive.nomachine.com box).

They plan to get to the point were you can have NX application servers running as a cluster of nodes, and users simply start an NX session locally and can select applications to run transparently (apps may even run on another NX node, but pretend to be on the same as used for initial login, because it displays in the same window. You also can run it full-screen, and after a short time you forget that it is a remote session at all).

Now the best thing for last: All the core compression and cachine technologies are released under the *GPL* and available as source code to anybody who wants to build on it! These technologies are working, albeit started from the command line only (and very inconvenient to use in order to get a fully running remote *X* session up and running).

To answer your questions:

+   • You do not need to install a terminal server; XP has RDP support built in.

+   • NX is much cheaper than *Citrix* — and comparable in performance, probably faster.

+   • You do not need to hack XP — it just works.

+   • You log into the XP box from remote transparently (and I think there is no need to change anything to get a connection, even if authentication is against a domain).

+   • The NX core technologies are all Open Source and released under the *GPL* — you can now use a (very inconvenient) command line at no cost, and you can buy a comfortable (proprietary) NX GUI front end for money.

+   • NoMachine is encouraging and offering help to *OSS/Free Software* implementations for such a front-end too, even if it means competition to them (they have written to this effect even to the LTSP, KDE, and GNOME developer mailing lists).

# ### 24.4 Network Logon Script Magic

There are several opportunities for creating a custom network start-up configuration environment.

+   • No Logon Script.

+   • Simple universal Logon Script that applies to all users.