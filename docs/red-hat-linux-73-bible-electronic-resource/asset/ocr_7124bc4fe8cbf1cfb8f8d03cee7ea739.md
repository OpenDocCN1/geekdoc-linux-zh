Replace user with the name of the user login that you have on the remote computer. (If you have the same user name on both computers, which is sometimes the case, you can skip the -l user option. The ssh command assumes your current login name.) You will be prompted for a password.

> NOTE: By default, the ssh service is not enabled in Red Hat Linux. The server (in this example, remote1) must consider the security consequences of enabling remote login services. Of the available choices, ssh is considered more secure than rlogin, telnet, or other login services.

+   4.  Type the password for the remote user login. (You are now logged in as the remote user in the Terminal window.)

+   5.  Set the DISPLAY variable on the remote computer to your local computer. For example, if your computer were named pine, the command would appear as:

```
$ export DISPLAY=pine:0
```

(If you are using a csh shell on the remote system, you may need to type setenv DISPLAY pine:0.)

+   6.  At this point, any X application you run from the remote system from this shell will appear on the local display. For example, to run a remote Terminal window so that it appears locally, type:

```
$ xterm -title "Terminal from Remote1"
```

The Terminal window appears on the local display with the word Remote1 in the title bar.

> TIP: As a rule, I use the -title option when I run remote X applications. In the title, I try to indicate the remote computer name. That way, I am reminded that the application is not running locally.

You need to remember some things about the remote application that is now appearing on your display:

+   -   If you only use the login to run remote applications, you can add the line exporting the DISPLAY variable to a user configuration file on the remote system (such as .bashrc, if you use the bash shell). After that, any application that you run will be directed to your local display.
+   -   Even though the application looks as though it is running locally, all the work is being done on the remote system. For example, if you ran a word processing program remotely, it would use the remote CPU and when you save a file, it is saved to the remote file system.

> CAUTION: Don't forget when a remote shell or file editor is open on your desktop. Sometimes people forget that a window is remote and will edit some important configuration file on the remote system by mistake (such as the /etc/fstab file). You could damage the remote system with this type of mistake.