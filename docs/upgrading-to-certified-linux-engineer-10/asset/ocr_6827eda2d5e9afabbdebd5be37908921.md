# Part III - Configure Automatically Home Directory Creation

+   1. Open the file /etc/pam.d/sshd with vi by entering
+   `vi /etc/pam.d/sshd`
+   2. Add the following line
+   `session required pam_mkhomedir.so skel=/etc/skel/ umask=0022`
+   3. Save the file and exit by entering `wq`.

# Part IV - Login as kbailey via SSH

+   1. Login as user kbailey by entering
+   `ssh -l kbailey localhost`
+   2. Enter yes to modify the list of known hosts.
+   3. Enter the password of kbailey (novell).
+   The home directory should be created.
+   4. Enter exit to log out.

(End of Exercise)