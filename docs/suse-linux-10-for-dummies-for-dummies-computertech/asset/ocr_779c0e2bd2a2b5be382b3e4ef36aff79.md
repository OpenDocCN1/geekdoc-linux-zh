Now I can make calls to anyone else with a SIP URL. For someone with a public IP address, I could make the call with a URL of the form `sip:username@IPAddress`, assuming that I know that person’s username and the system’s IP address.

![](bbox=[0.134, 0.216, 0.208, 0.287])

Another way to test Linphone on your own system (without having to call anyone else) is to type **sipomatic** in a terminal window. The program starts and prints some status messages. Then, type **sip:robot@localhost:5064** in the Linphone window and click the Call or Answer button. After a second, the **sipomatic** program should answer, and you should hear a short audio announcement over the speaker.

# Using Skype

Skype is another popular IP telephony application that uses proprietary peer-to-peer (P2P) protocol and has a large number of users. You can download Skype for SUSE Linux from `www.skype.com/products/skype/linux/`. What you download is an RPM file that you can install by typing **rpm -ivh skype-*.suse.i586.rpm** in a terminal window (after typing **su -** to become root). After that, you can start Skype by selecting Main Menu▸Internet▸More Programs▸Skype from the GUI desktop.

When you start Skype, Skype displays a dialog box that prompts you to log in. If you don’t have a Skype account yet, click the New Users tab (see Figure 10-17), fill in the required information, and click Next.

![](bbox=[0.231, 0.607, 0.608, 0.947])

**Figure 10-17:** You can register with the Skype service from this dialog box that appears when you run Skype.