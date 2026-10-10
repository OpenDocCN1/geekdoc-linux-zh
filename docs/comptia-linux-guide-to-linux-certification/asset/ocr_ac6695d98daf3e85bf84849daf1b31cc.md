+   3.  At the command prompt, type `systemctl enable sshd.service; systemctl start sshd.service` and press **Enter** to start the SSH daemon and ensure that it is started at boot time.

+   4.  At the command prompt, type `ssh root@localhost` and press **Enter**. When prompted to connect to the remote system, type **yes** and press **Enter**. Next, supply the root user’s password of LN XRocks! and press **Enter**.

+   5.  At the command prompt, type `who` and press **Enter**. Are you on a pseudoterminal? Type `exit` and press **Enter** to log out of your remote shell.

+   6.  Switch to a graphical terminal by pressing **Ctrl+Alt+F1** and log in to the GNOME desktop using the user name `user1` and the password of LN XRocks! . Next, open a command-line terminal (Activities, Show Applications, Utilities, Terminal).

+   7.  At the command prompt, type `ssh -X root@localhost` and press **Enter**. When prompted to connect to the remote system, type **yes** and press **Enter**. Supply the root user’s password of LN XRocks! and press **Enter** when prompted.

+   8.  At the command prompt, type `system-config-abrt` and press **Enter**. Note that this command starts the remote Problem Reporting Utility in a graphical window. Close the Problem Reporting Utility, type `exit`, and press **Enter** to close your remote shell. Log out of the GNOME desktop when finished.

+   9.  Switch back to try2 by pressing **Ctrl+Alt+F2** and type `ssh user1@IP`, where *IP* is the IP address of your Ubuntu Server Linux virtual machine. When prompted to connect to the remote system, type **yes** and press **Enter**. Supply the root user password of LN XRocks! when prompted. Why is the SSH daemon started by default in Ubuntu Server?

+   10. At the command prompt, type `su - root` and press **Enter**. Supply the root user password of LN XRocks! when prompted to obtain a root shell.

+   11. At the command prompt, type `vi /etc/ssh/sshd_config` and press **Enter**. Modify the **PermitRootLogin** without-password line such that it reads **PermitRootLogin yes**, save your changes, and quit the vi editor.

+   12. At the command prompt, type `service ssh reload` and press **Enter** to force the SSH daemon to reload its configuration file.

+   13. Type `exit` and press **Enter** to log out of your remote shell.

+   14. At the command prompt, type `ssh user1@IP`, where *IP* is the IP address of your Ubuntu Server Linux virtual machine, and supply the root user password of LN XRocks! when prompted. Next, type `exit` and press **Enter** to log out of your remote shell.

+   15. Supply the root user password of LN XRocks! when prompted. At the command prompt, type `ssh root@IP cat /etc/issue > /root/partner_issue` and press **Enter**, where *IP* is the IP address of your partner’s computer. Next, supply the root user’s password of LN XRocks! and press **Enter**.

+   16. At the command prompt, type `cat partner_issue` and press **Enter**. Was your partner’s issue file transferred successfully?

+   17. At the command prompt, type `less /etc/ssh/sshd_config` and press **Enter**. Examine the SSH client options available. Note the encryption algorithms supported in the commented Ciphers line. Press **q** when finished.