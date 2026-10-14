+   3. Add the RSA public key to your partner’s ~geeko/.ssh/authorized_keys file:
+      a. Using the password novell, copy the file to your partner’s home directory of geeko by entering the following:
+         `scp .ssh/id_rsa.pub geeko@partner_IP_address`
+      b. Log in as geeko to your partner’s computer using ssh by entering
+         `ssh -l geeko partner_IP_address`
+      c. Enter `ls -al`.
+         Look for an .ssh directory.
+      d. (Conditional) If an .ssh directory does not exist, create it by entering
+         `mkdir .ssh`
+      e. Copy the public key to the ~/.ssh/authorized_keys file by entering
+         `cat id_rsa.pub >> .ssh/authorized_keys`
+   
+   4. Log out from the partner’s computer by entering exit.
+   
+   5. Log in as geeko to your partner’s computer using ssh by entering
+      `ssh -l geeko partner_IP_address`
+      You are prompted for a passphrase, not a password.
+   
+   6. Log in by entering secret; then log out by entering exit.
+   
+   7. To track authentication, start the ssh-agent by entering
+      `ssh-agent bash`
+   
+   8. Add your private key to the agent for authentication by entering
+      `ssh-add .ssh/id_rsa`
+      Then enter a passphrase of secret.
+   
+   9. Log in as geeko to your partner’s computer using ssh by entering
+      `ssh -l geeko partner_IP_address`
+      This time you are not prompted for a password or a passphrase.
+   
+   10. Log out from your partner’s computer by entering exit.
+   
+   11. Switch to user root (su -, password n0v3ll).
+   
+   12. Open the /etc/ssh/sshd_config file in an editor of your choice, such as gedit.
+       a. Find the line containing PasswordAuthentication and make sure it is set to no.
+       b. Find the line containing UsePAM and change its setting from yes to no.
+       c. Save the file and close the editor.