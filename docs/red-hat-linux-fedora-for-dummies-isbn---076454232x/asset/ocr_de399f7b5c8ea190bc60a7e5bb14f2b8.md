# Reducing vulnerabilities by updating Red Hat Linux packages

Standard hacker operating procedure is simple: Find and then exploit vulnerabilities. The method, simple but effective, works like this: Joe Hacker walks around the Internet, rattling door knobs and occasionally finding one that's open. When no door is unlocked, the hacker looks for easier locks to pick. Your job is to make sure that your doors and windows are locked and not easily picked. Running firewalls, shutting down unnecessary services, and using good passwords ensures that you don't leave anything unlocked. Making sure that your locks are not easily defeated requires constant supervision. Software is now powerful but complex. Complexity breeds bugs, and with bugs come vulnerabilities. Because the only certainties in life are death, taxes, and buggy software, the bugs have to be fixed whenever possible. Everyone needs to continually update software when errors are found and corrected.

Red Hat created an excellent method for updating its software: The Up-to-Date (up2date) system automatically detects new software and installs it for you. Next to using good passwords and firewalls, it's probably the most effective security system you can run.

If you read about the Setup Agent (firstboot) post-configuration process in Chapter 3, you know that one of the Firstboot steps was registering with the Red Hat Network (RHN). You can register one computer with RHN at no cost. With RHN, you gain the ability to use up2date on one computer (you have to subscribe additional machines for a fee). Red Hat configures up2date to install new RPM packages daily.

You can register now if you haven't already done so. Follow these steps:

+   1. Click the GNOME menu, choose System Tools->Red Hat Network, and enter your root password if you're prompted.
The Welcome to Red Hat Update Agent window, as shown in Figure 17-1, opens.

+   2. Click the OK button and the Question dialog box opens.
You're told that your keyring doesn't contain the Red Hat public key. A keyring system helps maintain the public keys of places you need to securely communicate with. Because this is the first time you have tried to securely connect to the Red Hat Network, you don't have its public key.