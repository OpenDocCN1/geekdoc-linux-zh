+   6. Create and set the permissions for the `.ssh` directory with the following command:
+   
+   ```
+   mkdir .ssh ; chmod 700 .ssh
+   ```

+   7. Generate an RSA key:
+   
+   ```
+   ssh-keygen -b 1024 -t rsa
+   ```

+   8. When prompted for the location for the file, press Enter to accept the default.

+   9. When prompted for a passphrase, enter the following:
+   
+   ```
+   seatrc astronomy
+   ```

+   10. Reenter the passphrase when prompted.

+   11. Change into the `.ssh` directory and set the permissions on the `id_rsa.pub` file with these commands:
+   
+   ```
+   cd .ssh ; chmod 644 id_rsa.pub
+   ```

+   12. Copy the `id_rsa.pub` file to a new file called `authorized_keys`:
+   
+   ```
+   cp id_rsa.pub authorized_keys
+   ```

> > **NOTE**
> >
> > The next steps take place on the host **murphy**.

+   13. Ensure you can contact the host `fattyre` with a `ping`:
+   
+   ```
+   ping fattyre
+   ```

+   14. Sign on to the host `murphy` as the `root` user.

+   15. Add a user named `user2` with the following command:
+   
+   ```
+   useradd -m user2
+   ```

+   16. Set the password for `user2`:
+   
+   ```
+   passwd user2
+   ```

+   17. Enter the password twice to confirm it.

+   18. Switch to the `user2` account with this command:
+   
+   ```
+   su - user2
+   ```