![](bbox=[0.14, 0.06, 0.81, 0.4])

Figure 3-27 An application-oriented directory structure

# Implementing the Directory Structure

After creating volumes and designing directory structures, you're ready to start creating the directories shown on your volume and directory design forms. The directory structure can be created by using the local client computer's OS or by using Remote Manager. For example, from a client computer running Windows XP, you can map a drive to the NetWare volume and then create the network directory structure in My Computer or Windows Explorer, just as on a local hard drive. You can also use ConsoleOne or Remote Manager to create and work with the network directory structure. An advantage of Remote Manager is that it conforms to Novell's OneNet vision by allowing you to manage the file system from any client system or from a remote location.

Implementing the directory structure involves two main tasks: creating directories and subdirectories and setting directory space limitations with directory quotas. Because the Novell CNA exam requires you to know how to perform file system functions from Remote Manager, in the following activities you use this utility to create some of the Universal AeroSpace directories shown in Figure 3–25 and then set directory quotas on these directories.

# Activity 3-5: Creating a Directory Structure with Remote Manager

**Time Required:** 10 minutes

**Objective:** Create directories with Remote Manager.

**Requirements:** Same as Activity 3-1

**Description:** Eric wants you to implement a directory structure on the NetWare 6.5 server for evaluation purposes. He would like the directory structure to match the directory structure on the existing system. In this activity, you use Remote Manager to create part of the Universal AeroSpace directory structure shown in Figure 3–25.

+   1. If necessary, start Remote Manager using the IP address of your assigned NetWare 6.5 server.
+   2. Log in with your administrative user name and password.