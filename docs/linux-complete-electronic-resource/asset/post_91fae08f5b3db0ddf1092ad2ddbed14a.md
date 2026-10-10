
CIPE can be used in tunnelling, in order to create a Virtual Private Network. Low-level encryption has the advantage that it can be made to work transparently between the two networks connected in the VPN, without any change to application software.

Summarized from the CIPE documentation:

> The IPSEC standards define a set of protocols which can be used (among other things) to build encrypted VPNs. However, IPSEC is a rather heavy-weight and complicated protocol set with a lot of options, implementations of the full protocol set are still rarely used, and some issues (such as key management) are still not fully resolved. CIPE uses a simpler approach, in which many things which can be parameterized (such as the choice of the actual encryption algorithm used) are an install-time fixed choice. This limits flexibility, but allows for a simple (and therefore efficient, easy to debug) implementation.

Further information can be found at http://www.inka.de/~bigred/devel/cipe.html.

As with other forms of cryptography, it is not distributed with the kernel by default due to export restrictions.

## Kerberos

Kerberos is an authentication system developed by the Athena Project at MIT. When a user logs in, Kerberos authenticates that user (using a password), and provides the user with a way to prove her identity to other servers and hosts scattered around the network.

This authentication is then used by programs such as `rlogin` to allow the user to log in to other hosts without a password (in place of the `.rhosts` file). This authentication method can also be used by the mail system in order to guarantee that mail is delivered to the correct person, as well as to guarantee that the sender is who he claims to be.

Kerberos and the other programs that come with it prevent users from “spoofing” the system into believing they are someone else. Unfortunately, installing Kerberos is very intrusive, requiring the modification or replacement of numerous standard programs.

You can find more information about Kerberos by looking at the Kerberos FAQ (http://www.cis.ohio-state.edu/hypertext/faq/usenet/kerberos-faq/general/faq.html), and the code can be found at http://nii.isi.edu/info/kerberos.

From: Stein, Jennifer G., Clifford Neuman, and Jeffrey L. Schiller. “Kerberos: An Authentication Service for Open Network Systems.” USENIX Conference Proceedings, Dallas, Texas, Winter 1998.

Kerberos should not be your first step in improving security of your host. It is quite involved, and not as widely used as, say, ssh.

## Shadow Passwords

Shadow passwords are a means of keeping your encrypted password information secret from normal users. Normally, these encrypted passwords are stored in /etc/passwd file for all to read. Anyone can then run password guesser programs on them and attempt to determine what they are. Shadow passwords, by contrast, are saved in /etc/Shadow, which only privileged users can read. In order to use shadow passwords, you need to make sure all your utilities that need access to password information are recompiled to support them. PAM (above) also allows you to just plug in a shadow module; it doesn't require recompilation of executables. You can refer to the Shadow-Password HOWTO for further information if necessary. It is available at http://metalab.unc.edu/LDP/HOWTO/Shadow-Password-HOWTO.html. It is rather dated now, and will not be required for distributions supporting PAM.

## Crack and John the Ripper

If for some reason your passwd program is not enforcing hard-to-guess passwords, you might want to run a password-cracking program and make sure your users' passwords are secure.

Password cracking programs work on a simple idea: they try every word in the dictionary, and then variations on those words, encrypting each one and checking it against your encrypted password. If they get a match they know what your password is.

There are a number of programs out there–the two most notable of which are Crack and John the Ripper (http://www.false.com/security/john/index.html). They will take up a lot of your cpu time, but you should be able to tell if an attacker could get in using them by running them first yourself and notifying users with weak passwords. Note that an attacker would have to use some other hole first in order to read your `/etc/passwd` file, but such holes are more common than you might think.

Because security is only as strong as the most insecure host, it is worth mentioning that if you have any Windows machines on your network, you should check out *L0ph4Crack*, a Crack implementation for Windows. It’s available from http://www.10pt.com.

## CFS—Cryptographic File System and TCFS—Transparent Cryptographic File System

CFS is a way of encrypting entire directory trees and allowing users to store encrypted files on them. It uses a NFS server running on the local machine. RPMs are available at http://www.replay.com/redhat/, and more information on how it all works is at ftp://ftp.research.att.com/dist/mab/.

TCFS improves on CFS by adding more integration with the file system, so that it is transparent to users that the file system is encrypted. More information can be found at http://edu-gw.dia.unisa.it/tcfs/.

It also need not be used on entire filesystems. It works on directory trees as well.

## X11, SVGA, and Display Security

The following three sections discuss components of video security.

### X11

It’s important for you to secure your graphical display to prevent attackers from grabbing your passwords as you type them, reading documents or information you are reading on your screen, or even using a hole to gain root access. Running remote X applications over a network also can be fraught with peril, allowing sniffers to see all your interaction with the remote system.

X has a number of access-control mechanisms. The simplest of them is host-based: you use *xhost* to specify which hosts are allowed access to your display. This is not very secure at all, because if someone has access to your machine, they can *xhost + their machine* and get in easily.

Also, if you have to allow access from an untrusted machine, anyone there can compromise your display.

When using xdm (X Display Manager) to log in, you get a much better access method: MIT-MAGIC-COOKIE-1. A 128-bit cookie is generated and stored in your .Xauthority file. If you need to allow a remote machine access to your display, you can use the xauth command and the information in your .Xauthority file to provide access to only that connection. See the Remote-X-Apps mini-HOWTO, available at http://metalab.unc.edu/LDP/HOWTO/mini/Remote-X-Apps.html.

You can also use ssh to allow secure X connections. This has the advantage of also being transparent to the end user, and means that no unencrypted data flows across the network (see the section, "ssh [Secure Shell] and stlnter").

Take a look at the Xsecurity man page for more information on X security. The safe bet is to use xdm to log in to your console and then use ssh to go to remote sites on which you wish to run X programs.

### SVGA

SVGAlib programs are typically SUID-root in order to access all your Linux machine's video hardware. This makes them very dangerous. If they crash, you typically need to reboot your machine to get a usable console back. Make sure any SVGA programs you are running are authentic, and can at least be somewhat trusted. Even better, don't run them at all.

### GGI (Generic Graphics Interface project)

The Linux GGI project is trying to solve several of the problems with video interfaces on Linux. GGI will move a small piece of the video code into the Linux kernel, and then control access to the video system. This means GGI will be able to restore your console at any time to a known good state. They will also allow a secure attention key, so you can be sure that there is no Trojan horse login program running on your console (see http://synergy.caltech.edu/~ggi/).

## KERNEL SECURITY

This is a description of the kernel configuration options that relate to security, and an explanation of what they do, and how to use them.
