
In all modern versions of Windows, Microsoft thoughtfully includes a command-line FTP program virtually identical to the ftp command in Linux. You can access your host computer's FTP server by opening an MS-DOS window (or command prompt, depending on your version of Windows) and typing ftp IP_address_of_host. If your Windows VM is only running host-only or bridged networking, but not both, be sure to use the appropriate host IP.

You might want something a little more robust if FTP is going to be your primary method for sharing files between Linux and your Windows guest. WS_FTP, from Ipswitch, Inc. (http://www.ipswitch.com) is one of the leading graphical, easy-to-use FTP programs. You might also consider LeechFTP, a freeware, "power user" oriented FTP client. LeechFTP on a Windows 98 virtual machine is shown in Figure 9.1.

> LeechFTP is available from http://linux.fh-heilbronn.de/~debis/leechftp.

If you're concerned about the security issues of opening an FTP server on your desktop, you can run the FTP server on the virtual machine instead. Although it's not as efficient to run server software on a guest VM, it is more secure (because fewer people know of the existence of the VM, and it's probably not running all the time). For added protection, you can run the server on a VM that has host-only networking, which makes it effectively off-limits to the rest of the world.

![](img/b2b6702758c230ce537468351fc8af15_172_0.png)

Figure 9.1 An FTP client is an efficient way to move files to and from your virtual machine.

> Many Windows server programs answer requests over both bridged and host-only networking, so if you have both types of networking installed on the Windows virtual machine, the outside LAN will be able to access the server software.

Windows NT and 2000 Server have specialized server-class FTP servers you might investigate if you need to test a production environment. But for general, file-swapping, light-duty use, a shareware server such as Dragon Server fits the bill just fine for any 32-bit version of Windows.

Here's how you get Dragon Server up and running:

> You need a program that handles zip file archives, such as WinZip or PKZip for Windows, to install Dragon Server. You can download one from a shareware site such as http://www.hotfiles.com or http://www.download.com.

- 1. Start your Windows VMware session, if you haven't already.
- 2. Insert the included CD in the drive.
- 3. Using My Computer or Windows Explorer, open the CD and browse to the Extras/Windows directory.
- 4. Double-click the drgnsrvr.zip archive to open the file (see Figure 9.2).
- 5. Copy the contents to a temporary installation folder.
- 6. Double-click the Setup icon to start the installation. The Dragon Server license agreement is displayed. Read it and then close it to proceed.
- 7. Change the installation directory if you desire, type your name and email address in the provided boxes shown in Figure 9.3, and then click Continue.

![](img/b2b6702758c230ce537468351fc8af15_173_0.png)

Figure 9.2 Dragon Server comes in a small ZIP archive.

![](img/b2b6702758c230ce537468351fc8af15_174_0.png)

Figure 9.3 Installing Dragon Server requires a short registration step.

8. The next window is the Server configuration (see Figure 9.4). You can leave the Server home directory alone, but be sure to click the box next to FTP to enable FTP service and set Max Users to something greater than 0. If you don't make both changes, you won't be able to connect to the FTP server!

![](img/b2b6702758c230ce537468351fc8af15_174_1.png)

Figure 9.4 Be sure to enable FTP access and permit more than zero users to log in.

9. Locate the Dragon Server program group (it should be in its own group under Programs on the Windows Start menu) and launch the server.

10. Before you can FTP into your Windows virtual machine, you need to set up at least one login name. Click Users in the toolbar, and select Options to open the User Settings window, shown in Figure 9.5.

![](img/b2b6702758c230ce537468351fc8af15_174_2.png)

Figure 9.5
