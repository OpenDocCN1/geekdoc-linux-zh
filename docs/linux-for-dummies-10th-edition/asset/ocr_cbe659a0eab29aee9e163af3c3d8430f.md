# Setting up and making your SSH connection in Windows

Using PuTTY is almost as easy as downloading it. From the main PuTTY window:

+   1. Click Session in the left side menu to show the session options. Refer to Figure 18-3.

+   2. Type the hostname or IP address of the remote computer you want to connect to in the text box at the top of the window.

If you're not sure of the address of your Linux system, open a Terminal prompt and type the command ip addr. You should see the IP address assigned to the Ethernet port.

+   3. Ensure the SSH radio button under the address is selected (this should already be selected by default).

+   4. If you want to save the connection settings, put a name in the Save Sessions text box and click Save.

You can select the saved session from the list box. PuTTY restores all the configuration settings to what you had saved.

+   5. Click the Open button to start the SSH session.

The first time you connect to your Linux system, PuTTY prompts whether you want to save the fingerprint key for the server. This ensures another server on the network doesn’t steal your server’s IP address and hijack your connection. Just click Yes to accept the key.

PuTTY emulates a console terminal as it presents the command line from the remote system. You can change the appearance of the terminal window by clicking the Appearance entry under the Window section of the main PuTTY window, as shown in Figure 18–4.

![](bbox=[0.15, 0.93, 0.24, 0.99])

If you use virtualization software to run your Linux workstation as a virtual machine (see Chapter 20), make sure you select the option to create a bridged network connection rather than a NAT network connection. The NAT network connection assigns an IP address to your Linux workstation that’s not on your local network, and you won’t be able to connect to it from a remote client.

The terminal emulation window then appears, asking you for the userid and pass-word to use for the connection. After entering your login information, you should get a command line prompt for the remote computer, as shown in Figure 18–5.