Table 4-4 Novell clients (continued)

| **Novell Client Version** | **Description** |
| :--- | :--- |
| Client 32 | Client 32, an early version of Novell Client, was used with Windows 95. Like the NetX client, Client 32 depended on IPX/SPX to access NetWare servers. Client 32 used the capabilities of a 32-bit OS to enhance the client's features and performance. Because OSs such as Windows 9x, 2000, and XP are more network aware than DOS, Client 32 worked with the OS to provide access to NetWare services instead of acting as a DOS shell. |
| Novell Client | Novell Client is an improved version of Client 32 that provides access to NetWare services by using IPX/SPX or TCP/IP. Versions of Novell Client are available for Windows-based computers. The latest Novell Client is required if you need to use NetWare 6.5 management tools, such as ConsoleOne, and access application services, such as Z.E.N.works. |

Installing Novell Client from a CD on every computer in a network is usually too time consuming. Fortunately, Novell offers multiple installation or upgrade methods to make this job easier. As a network administrator, you can select any of the following methods to install Novell Client, depending on the computer's configuration and your personal preferences.

+   - **Install from CD-ROM**—This method is best used on new computers that aren't currently connected to the network. If the computer has a CD-ROM drive, Novell Client can be installed quickly from the Client CD.
+   - **Install from the network**—Another good use of Novell NFAP is installing Novell Client on a new Windows computer. With NFAP, a new computer can log in to the network using only the default Microsoft NetWare client. Novell Client can then be installed from a shared copy of the client installation software on the NetWare server. Installing from the network is faster and more convenient than installing from a CD. For example, when setting up a new computer for the UAS organization, Eric often installs Novell Client from a shared network directory on the NetWare server instead of from the Client CD. With this method, he can install several clients at the same time without having multiple copies of the Client CD. To do this, Eric uses the Microsoft client on the new computer to access the Novell Client folder on the NetWare 6.5 server.
+   - **Automatic Client Upgrade (ACU)**—You can use the ACU method to automate upgrading older Novell Client versions to the latest Novell Client when a user logs in from the computer. The ACU method involves placing special commands in the container login script file, as described in Chapter 9, that starts the upgrade. This method can be a little tricky to set up, but it's helpful when you're upgrading multiple computers to the latest version of Novell Client.

# Activity 4-6: Installing Novell Client

**Time Required:** 15 minutes

**Objective:** Install Novell Client.

**Requirements:**

+   - A Windows XP computer
+   - A user name and password that has administrative rights to your Windows system
+   - A copy of the Novell Client CD version 4.91 or later

**Description:** In this activity, you learn how to install Novell Client using a CD or a network directory. If you're using a classroom server, your instructor will provide the location of the Novell Client files on the classroom server. If you're using a dedicated server, this activity should be performed using the Novell Client CD. To change your Windows XP network configuration in this activity, you need to log on to your local Windows computer with a user name and password that has administrative privileges.