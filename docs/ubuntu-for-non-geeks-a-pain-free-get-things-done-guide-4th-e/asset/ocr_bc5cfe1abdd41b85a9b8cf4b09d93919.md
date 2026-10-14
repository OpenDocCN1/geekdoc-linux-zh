# Taking Control of Firestarter

You can control how Firestarter deals with various network events by creating your own policies. The default policy set in Firestarter allows you to do whatever you normally do via the Internet, while it blocks new connections to your computer from the Internet or any other computer on your network.

To make things a bit more draconian, you can click the Policy tab, select Outbound traffic policy in the Editing drop-down menu, and then select Restrictive by default, whitelist traffic. If you just want to deny anyone working on your computer access to a specific website, for instance, simply select Permissive by default, blacklist traffic, right-click the Deny connections to host field, and select Add Rule in the pop-up menu. In the Add new outbound rule window, enter the domain name for the targeted site (as in example.com), click Add, and then click the Apply Policy button in the main Firestarter window (it’s the one that looks like a green check mark).

# Confirming That Firestarter Runs Automatically

After you run Firestarter the first time, it will set itself to automatically start up whenever you start your system. Don’t be concerned when you don’t see the graphical interface you saw when you first started it; Firestarter will be running in the background, silently protecting your computer.

If you are the doubting type, you can check to see whether Firestarter actually is running in the background by opening a Terminal window, typing sudo /etc/init.d/firestarter status, and then pressing ENTER. If Firestarter is running, you will see the message * Firestarter is running... in the Terminal window. Worries over. If Firestarter isn’t running, the response will read * Firestarter is stopped.

# Finding Out More

If the world of firewalls is new to you, you can check out the Firestarter home page to learn a bit more. To check out the online manual, just go to the Firestarter Help menu, and select Online Users’ Manual, which will open the page in your web browser. If you prefer to check out the manual before installing Firestarter, point your browser to http://www.fs-security.com/docs/. You will also find a pretty good quick tutorial there.

# ClamAV: Antivirus Software, Linux Style

Despite the lack of viruses that can wreak havoc upon your Linux system, your computer could still act as a transmitter of Windows viruses. As a result, a number of free antivirus scanners are available for Linux users interested in helping protect Windows users from viruses. These include Panda Desktop Secure (http://www.pandasecurity.com/usa/homeusers/downloads/desktopsecure/), f-Prot (http://www.f-prot.com/), and numerous others. For most Linux users, however, the virus scanner of choice is the open source contender: ClamAV.