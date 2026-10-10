![](bbox=[0.16, 0.07, 0.96, 0.51])

# Harden the Bootloader Program

+   7. Type the command: `su -c 'vi /boot/grub/grub.conf'` and press `\<enter>`. When prompted, enter the password for root (`ISS316Security`).
+   
+       ```text
+       [student@TargetFedora01 ~]$ su -c 'vi /boot/grub/grub.conf'
+       Password:
+       ```
+       
+       Figure 1 — *Opening grub.conf as the root user*
+   
+   8. Verify the grub menu’s timeout is set to `0`.
+       
+       ```text
+       timeout=0
+       ```
+   
+   9. Exit the file. Hit the `Esc` and `:` keys to enter command mode. At the colon prompt in command mode, type `q` to exit the file.
+   
+   10. Enter the grub console. Type the command: `grub` and press `\<enter>`.
+   
+   11. The prompt will appear as `grub>\`.
+   
+   12. Create a md5 password. Type the command: `md5crypt` and then press `\<enter>`