![](bbox=[0.08, 0.12, 0.78, 0.43])

Figure 15-4 Establishing an X Windows Connection

This command starts a **dterm** window, which is a standard window program on UNIX with a white background, and displays the window on the system at the IP address 15.32.165.11. The IP address in this case is the Windows system on which you are issuing the command, which is the X Windows server. The ":0" indicates that the first display on the Windows system will be used for **dterm**, because in the X Windows world, you can have several displays on a system. The system on which the command runs is 15.32.165.10. This is the UNIX system that acts as the X Windows client.

Although you are typing this information on your Windows system, this command is being transferred to the UNIX system you specified in the *Xstart* box. This transfer will have the same result as typing the **dterm** command shown on the UNIX system directly.

When you type your password and click *OK*, a **dterm** window appears on your Windows system that is a window into your UNIX