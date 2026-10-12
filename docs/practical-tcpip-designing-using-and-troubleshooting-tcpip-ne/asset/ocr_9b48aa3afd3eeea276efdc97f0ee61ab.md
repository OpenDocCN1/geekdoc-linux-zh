# ## 20.11 Logon and controlling access to network resources

When you have logged on successfully, your logon account controls which resources you may access. Here we give a (very brief) summary of the internal mechanisms used to implement this.

+   1. when the MSV1_0 authentication package retrieves the hashed password from the SAM database (local logon in Module 20.3, network logon in Module 20.8) it also retrieves from the database the *security ID (SID)* for your username, and SIDs for all groups that you belong to. A security ID is a unique number used to represent a user or group; you can think of it as a numeric name
+   2. MSV1_0 returns all these SIDs to the LSA (Local Security Authority) on the machine you’re sitting at (logging in from)
+   3. the LSA creates an *access token* containing all the SIDs and a list of all the associated user rights
+   4. the LSA passes the access token to **WinLogon**
+   5. **WinLogon** runs your desktop (usually starting with Windows Explorer) and the access token is attached to that process
+   6. any process that you start after this also inherits a copy of the token.

All the above happens when you logon.

Now, when one of your processes attempts to use a resource on the local machine, e.g. read a particular file:

+   7. the *Security Reference Monitor* component in the NT kernel checks your access token against the *access control list (ACL)* for the resource, and decides whether you are allowed to access it. An ACL is simply a list saying which users and groups are allowed to do what with this resource; you modify a file’s ACL, for example, using the File > Properties dialog for the file in Windows Explorer (Figure 20.12).

**Figure 20.12**
Modifying a file’s access control list

![](bbox=[0.29, 0.6, 0.9, 0.94])