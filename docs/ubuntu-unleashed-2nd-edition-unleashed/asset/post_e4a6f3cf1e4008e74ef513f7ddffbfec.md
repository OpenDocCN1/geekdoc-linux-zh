
To set up VNC, start Synaptic and install the vnc-common and xvncviewer packages. With that done, all that remains is to tell Ubuntu who should be allowed to connect to your session. This is done from the Remote Desktop option on the Preferences menu. By default, your desktop is not shared, so check Allow Other Users to View Your Desktop to share it. You should also check Allow Other Users to Control Your Desktop; otherwise, people will be able to see what you are doing but not interact with the desktop—which is not very helpful.

The second set of options on that screen is important. If you are using this as a remote way to connect to your own desktop, deselect Ask You for Confirmation. If this is not done, when you try to connect from your remote location, Ubuntu will pop up a message box on the local machine asking Should this person be allowed to connect? Because you are not there to click Yes, the connection will fail. If you want to let someone else remotely connect to your system, keep this box enabled so you know when people are connecting. You should always enter a password, no matter who it is that will connect. VNC, like XDMCP, should not be considered secure over the Internet, or even on untrusted networks.

## Reference

- http://www.openssh.com—The home page of the OpenSSH implementation of SSH that Ubuntu uses. It is run by the same team as OpenBSD, a secure BSD-based operating system.
- http://www.realvnc.com—The home page of the team that made VNC at AT&T’s Cambridge Research Laboratory. It has since started RealVNC Ltd., a company dedicated to developing and supporting VNC.
- http://www.tightvnc.com—Here you can find an alternative to VNC called TightVNC that has several key advances over the stock VNC release. The most important feature is that TightVNC can use SSH for encryption, guaranteeing security.
- http://www.nomachine.com/—Another alternative to VNC is in the pipeline, called NX. The free implementation, FreeNX, is under heavy development at the time of writing but promises to work much faster than VNC.

One book on SSH that stands out from the crowd is known as “The Snail Book” because of the picture on the cover. It covers all the SSH suite and is called SSH: The Secure Shell (O’Reilly), ISBN: 0-596-00011-1.

## PART III

## Ubuntu as a Server

## IN THIS PART

- CHAPTER 20 Apache Web Server Management 443
- CHAPTER 21 Administering Database Services 481
- CHAPTER 22 File and Print 509
- CHAPTER 23 Remote File Serving with FTP 535
- CHAPTER 24 Handling Electronic Mail 579
- CHAPTER 25 Proxying and Reverse Proxying 597
- CHAPTER 26 LDAP 607

## CHAPTER 20

## Apache Web Server Management

## IN THIS CHAPTER

This chapter covers the configuration and management of the Apache web server. The chapter includes an overview of some of the major components of the server and discussions of text-based and graphical server configuration. You will see how to start, stop, and restart Apache using the command line. The chapter begins with some introductory information about this popular server and then shows you how to install, configure, and start using Apache.

## About the Apache Web Server

Apache is the most widely used web server on the Internet today, according to a Netcraft survey of active websites in January 2005, which is shown in Table 20.1.

Note that these statistics do not reflect Apache's use on internal networks, known as intranets.

The name Apache appeared during the early development of the software because it was "a patchy" server, made up of patches for the freely available source code of the NCSA HTTPd web server. For a while after the NCSA HTTPd project was discontinued, a number of people wrote a variety of patches for the code, to either fix bugs or add features they wanted. A lot of this code was floating around and people were freely sharing it, but it was completely unmanaged.

After a while, Brian Behlendorf and Cliff Skolnick set up a centralized repository of these patches, and the Apache project was born. The project is still composed of a small core group of programmers, but anyone is welcome to submit patches to the group for possible inclusion in the code.

- About the Apache Web Server
- Installing the Apache Server
- Starting and Stopping Apache
- Runtime Server Configuration Settings
- File System Authentication and Access Control
- Apache Modules
- Virtual Hosting
- Logging
- Dynamic Content
- Other Web Servers for Use with Ubuntu
- Reference
