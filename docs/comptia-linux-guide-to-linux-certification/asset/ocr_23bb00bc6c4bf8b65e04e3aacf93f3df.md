+   5. Switch to a command-line terminal (tty5) by pressing **Ctrl+Alt+F5** and attempt to log in to the terminal using the user name of **bozo** and the password of **LNXRocks!**. Were you successful?

+   6. Switch back to the command-line terminal (tty2) by pressing **Ctrl+Alt+F2**.

+   7. At the command prompt, type `passwd -u bozo` and press **Enter** to unlock bozo’s user account.

+   8. At the command prompt, type `cat /etc/shadow` and press **Enter**. Compare the encrypted password for bozo’s user account to the one recorded in Step 2.

+   9. Switch to a command-line terminal (tty5) by pressing **Ctrl+Alt+F5** and attempt to log in to the terminal using the user name of **bozo** and the password of **LNXRocks!**. Were you successful?

+   10. Type `exit` and press **Enter** to log out of your shell.

+   11. Switch back to the command-line terminal (tty2) by pressing **Ctrl+Alt+F2**.

+   12. At the command prompt, type `csh -s /bin/false bozo` and press **Enter** to change bozo’s shell to `/bin/false`. What message did you receive? Was the shell changed? Type `cat /etc/passwd` at a command prompt to verify that the shell was changed to `/bin/false` for bozo’s user account.

+   13. Switch to a command-line terminal (tty5) by pressing **Ctrl+Alt+F5** and attempt to log in to the terminal using the user name of **bozo** and the password of **LNXRocks!**. Were you successful?

+   14. Switch back to the command-line terminal (tty2) by pressing **Ctrl+Alt+F2**.

+   15. At the command prompt, type `csh -s /bin/bash bozo` and press **Enter** to change bozo’s shell to `/bin/bash`.

+   16. Switch to a command-line terminal (tty5) by pressing **Ctrl+Alt+F5** and attempt to log in to the terminal using the user name of **bozo** and the password of **LNXRocks!**. Were you successful?

+   17. Type `exit` and press **Enter** to log out of your shell.

+   18. Switch back to the command-line terminal (tty2) by pressing **Ctrl+Alt+F2**.

+   19. Type `exit` and press **Enter** to log out of your shell.

# **Project 10-8**

In this hands-on project, you remove a user account on Fedora Linux and create a new user account in its place using command-line utilities.

+   1. On your Fedora Linux virtual machine, switch to a command-line terminal (tty2) by pressing **Ctrl+Alt+F2** and log in to the terminal using the user name of **root** and the password of **LNXRocks!**.

+   2. At the command prompt, type `ls -la /home/bozo` and press **Enter**. Who owns most files in this directory? Why?

+   3. At the command prompt, type `userdel bozo` and press **Enter**. Was the home directory removed for bozo as well?