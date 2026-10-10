# Working with the Secure Shell Protocol: OpenSSH

Many users and network administrators of Linux-based systems are familiar with utilities such as Telnet, Rlogin (remote login), and FTP to access servers and transfer files. However, these utilities have the disadvantage of transmitting information across the local network or Internet unencrypted. With NetWare 6.5 OES, Novell has integrated an open-source solution to this problem by including OpenSSH. OpenSSH offers the same functions as Telnet, Rlogin, and FTP but includes encryption to protect data and passwords from eavesdropping, connection hijacking, and other attacks. Using OpenSSH, Novell developers and administrators can access data on NetWare servers securely by using Novell International Cryptographic Infrastructure (NICI), as described earlier. With the Secure Shell protocol (SSH), you can gain remote access to any server in the network running the OpenSSH service. OpenSSH includes the following utilities:

+   - SSH, which replaces Rlogin and Telnet
+   - SCP, which replaces RCP
+   - S/FTP, which replaces FTP
+   - OpenSSH Manager, which can be accessed via a Web browser and used to view SSH connections, change the Sshd.config file, and set log preferences; enables any user who is a member of the Ssh admin Administrators group in eDirectory to modify the configuration of OpenSSH servers

SSH is used with remote login and file transfer programs, such as Telnet and FTP, to provide an encrypted link between the client and server. SSH uses public key cryptography to establish an encrypted secure connection between the user and the remote system. After the secure connection is established, user names, passwords, and all other data can be transmitted securely over the connection. Because of its popularity, many network applications and OES, including NetWare 6.5, now support SSH ports, and free clients are available for logging on to an SSH-compatible server. In the following activity, you learn how to install OpenSSH on your NetWare 6.5 server.

> NOTE If you're using a shared classroom server, your instructor might perform this activity as a class demonstration.

# Activity 11-7: Installing OpenSSH

Time Required: 10 minutes

Objective: Use the NetWare server's graphical console to install the OpenSSH service.

Requirements: A dedicated NetWare 6.5 server

Description: To allow users to download files securely from the FTP site, Eric wants to use S/FTP. In this activity, you install OpenSSH on your server console.

+   1. At the NetWare 6.5 server’s graphical console, click the **Novell** button and then click the **Install** option to display a list of installed services.
+   2. Insert your NetWare 6.5 Products CD 2 into the server’s CD-ROM drive, and then click the **Add** button.
+   3. Click the **browse** button, navigate to the **NW65PROD** CD, and click it to display the Postinst.nif file. Click the **Postinst.nif** file and click **OK** to see a list of product options.
+   4. When the product list window is displayed, click the **Clear All** button, and then scroll down and click to select the **OpenSSH** check box.
+   5. Click **Next** and then click **Copy files** to copy the files and complete the installation. If requested, log in with your administrative user name and password.
+   6. After the installation is finished, click the **Reset Apache** button to reload your Apache administrative server.