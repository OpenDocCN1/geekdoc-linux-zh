If at boot your kernel reports messages like
PP Dynamic channel allocation code copyright 1995 Caldera, Inc.
PPP line discipline registered.

your kernel does have PPP support compiled in.

That said, you will probably want to compile your own kernel whatever your distribution to provide the most efficient use of system resources given your particular hardware configuration. It is worth remembering that the kernel cannot be swapped out of memory and so keeping the kernel as small as possible has advantages on a memory limited machine.

This document provides minimal kernel recompilation instructions in the section, “Configuring Your Linux Kernel.”

For greater detail, see the Kernel-HOWTO at The Linux Kernel HOWTO (http://MetaLab.unc.edu/mdw/HOWTO/Kernel1-HOWTO.html).

# Obtaining Information from Your ISP

There are an almost infinite number of ways in which a PPP server can be set up. In order to connect to your ISP (or corporate PPP server to access your intranet), you will need to obtain information on how the PPP server operates.

Because you are using Linux, you may have some difficulty with some ISP help-desks (and work-site-based PPP intranet servers) which know only about MS Windows clients.

However, a rapidly growing number of ISPs use Linux to provide their service—and Linux is also penetrating the corporate environment as well, so you may be lucky if you do strike problems.

The section, “Getting the Information You Need about the PPP Server,” tells you what you need to know about the PPP server to which you are going to connect—and how to find out the information you need to know.

# Configuring Your Modem and Serial Port

In order to connect to a PPP server and to obtain the best possible data transfer rate, your modem needs to be configured correctly.

Similarly, the serial ports on your modem and computer need to be set up correctly.

The section, “Configuring Your Modem and Serial Port,” provides information on this.