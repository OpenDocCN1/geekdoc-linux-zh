+   - **Host with permanent network connection (SMTP)**—You can use this if your system has a permanent connection to the Internet.
+   - **Single user machine without network connection**—Use this option if your machine doesn't have a network connection. You might be wondering why in the world you would set up a mailing system if you didn't have a network connection. Several of your applications send you internal mail messages to report progress and errors. Remember, even when Linux is not connected to a network, there is a network inside it.
+   - **Host with temporarily network connection (Modem or ISDN)**—Use this configuration if you have a dial-up connection. This enables you to use your machine as a mail server, and when you connect, your email will be sent.
+   - **Use UUCP to send mail**—If you will be connecting to a network, choose this configuration so you can send email.
+   - **Expert mode for sendmail configuration**—Proceed with caution when choosing this configuration; it should be used only by experts.

Use the arrow keys to highlight the configuration you want to use and press Enter to continue.

YaST now takes over completely and starts to configure your system based on your answers to the previous questions. YaST launches SuSEConfig, which configures your system for you (see Figure 2.31).

FIGURE 2.31
YaST launches SuSEConfig to configure your system.

![](bbox=[0.32, 0.62, 0.7, 0.88])

When SuSEConfig is finished, press Continue to proceed. YaST tells you that your system is now installed successfully and will be started (see Figure 2.32). Press Enter to start your system for the first time.

The system boots up directly with no computer restart necessary. Figure 2.33 shows a system booting up for the first time.