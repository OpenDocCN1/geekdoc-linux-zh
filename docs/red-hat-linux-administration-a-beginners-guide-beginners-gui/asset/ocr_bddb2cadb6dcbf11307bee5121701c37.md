project was born. More significant than the cost of the package is the fact that the source code to the package is completely open. This is important to cryptographic software, for it allows peers to examine the source code and make sure that there are not holes that may allow crackers to break the security. (In other words, serious cryptographers do not rely on security through obscurity.)

Because the SSH protocol has become an Internet Engineering Task Force (IETF) standard, there are also other developers actively working on SSH clients for other operating systems. There are many Windows, Macintosh, and Palm Pilot clients, in addition to the standard UNIX clients. You can find the version of OpenSSH that we will be discussing at http://www.openssh.org. You can find other implementations of SSH at http://www.ssh.com.

![](bbox=[0.15, 0.35, 0.25, 0.42])

> As of this writing, we are up to SSH protocol version 2. Unfortunately, many non-UNIX clients support or enable only the SSH version 1 protocol. Thus it is important that your server side understand both versions. You should default to version 2 whenever possible because it is considered to be more secure than version 1. Use version 1 only in situations where version 2 is not available. If you plan to use OpenSSH, don’t worry, it supports both.

# OpenSSH and OpenBSD

The OpenSSH project is being spearheaded by the OpenBSD team. OpenBSD is a version of the BSD operating system (another UNIX variant) that strives for the best security of any operating system available. A quick trip to the OpenBSD web site (http://www.openbsd.org) shows that the organization has had only one remote hole in its default installation in nearly six years. Unfortunately, this comes at the expense of not having the most whiz-bang, feature-rich tools available, as the organization requires that anything added to its distribution get audited for security first. This has made OpenBSD a very popular foundation for applications such as firewalls.

The core of the OpenSSH package is considered part of the OpenBSD project and is, therefore, very simple and specific to the OpenBSD operating system. To make OpenSSH available to other operating systems, a separate group exists to make OpenSSH portable whenever new releases occur. Typically, this takes only a few days from the original release. (For instance, OpenSSH 3.4 and OpenSSH 3.4.p1, the portable version—one containing support for both SSH1 and SSH2—were released the same day.)

![](bbox=[0.15, 0.84, 0.25, 0.91])

> Since we are targeting Linux, we will use the versions suffixed with a p indicating that it has been ported.