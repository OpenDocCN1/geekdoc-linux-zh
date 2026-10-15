The original Red Hat 6.0 shipped with Samba version 2.0.3, but version 2.0.5a has subsequently been released. Because Red Hat has made a 2.0.5a update available, and because the CD that accompanies this book installs that updated version by default, that's the version described in this chapter. Previous versions of Red Hat shipped with pre-2.0 varieties of Samba, and if you're using an older distribution, you might have such a version. I recommend that you upgrade Samba in this situation.

> NOTE
> If Samba is not already installed on your computer, install it now. On an RPM-based system, type rpm -q samba to see if it's installed.

Samba is a very complex software package, with lots of subtleties. This chapter can get you started using it, but it doesn't cover every aspect of the server. For basic information on the commands and options you don't find here, you can start by reading the manpages for smb.conf, smbd, or any other relevant tool. You can also check the documentation in the /usr/doc/samba-2.0.5a directory, and on the Samba Web site, http://samba.org. If you need to delve deeper into Samba, you might want to check out Sams Teach Yourself Samba in 24 Hours, which goes into far more detail than one chapter can.

# Samba: NetBIOS over TCP/IP for Linux

In the 1980s, IBM developed a networking technology that it called NetBIOS (Network Basic Input/Output System) for small networks of PCs. This technology has grown and transformed in various ways over the years, and is now an important component of Windows workgroup networking, and thus for Samba.

# Understanding NetBIOS and NetBEUI

If you've configured Windows computers, you've no doubt seen the terms NetBIOS and NetBEUI in reference to Windows networking protocols, but you may not know what they are. NetBIOS, as mentioned, is the core of the Windows networking protocols. NetBEUI stands for NetBIOS Extended User Interface, and is both an extension of NetBIOS and a networking layer upon which NetBIOS rests.