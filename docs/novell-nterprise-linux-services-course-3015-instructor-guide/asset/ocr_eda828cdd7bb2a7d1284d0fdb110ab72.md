+   4.  Apply the necessary ownerships and permissions to the new parent directory. The assigned owner should be **novlvww** and the assigned group should be **novlvww**. The permissions should be **700**.
+   
+   For example, enter the following commands:
+   
+   -   **ls -1 /home/ifolderdata** (to see the current ownership and permission settings)
+   -   **chown novlvww:novlvww /home/ifolderdata**
+   -   **chmod 700 /home/ifolderdata**
+   -   **ls -1 /home/ifolderdata** (to see the changes made to the ownership and permission settings)
+   5.  Restart **novell-httpd**, by entering **/etc/init.d/novell-httpd restart**.

# ### How to Install and Configure the iFolder Client

You install the Novell iFolder Client software on each desktop or laptop that you typically use. The iFolder client is designed for workstations in the following Microsoft® operating environments:

+   -   Windows 98/ME
+   -   Windows XP Home and Professional
+   -   Windows 2000 Professional

You need the iFolder client on your workstation to take advantage of the automatic synchronization feature of iFolder. However, you can access your files on the iFolder server from any computer using a web browser and an active Internet connection.