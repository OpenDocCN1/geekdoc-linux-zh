Port 80 is used to send the encrypted username and password and data from the iFolder client to the iFolder server.

iFolder uses RSA* encryption to encrypt the username and password, and Blowfish* encryption to encrypt the user data. Port 443 is used to access the iFolder Management console and the Java applet via SSL and HTTPS.

+   4. When you finish, add the server by selecting **Add**.

# ## Set Global Server Policies

You can regulate how much disk space will be allotted to each iFolder user or how much time will pass before a session times out by doing the following:

+   1. Log in to the Global Settings section of the iFolder Management console with your Admin *username* and *password*.
+   2. Select **Global Policies**; then select the **Display** button next to Server Policies.
+   The following appears:

![](bbox=[0.07, 0.45, 0.91, 0.62])

+   3. Complete the following information:
+       *   **Initial Client Quota.** Specify the amount of storage space (in MB) that will be the minimum amount assigned to new iFolder user accounts.