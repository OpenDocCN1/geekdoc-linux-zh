# Security

also share the same numeric ID although they are for the User ID (UID) and Group ID (GID). Your home directory is automatically set to allow you full access as a user, and to allow read access only to members of your group. This isn’t particularly secure, so to start off with we’d suggest changing the permissions on your home directory so that access is denied to Others. To do this, go to Places > Computer, and navigate into the Home directory. Right-click on your user home directory and select properties. In the window that appears, click the Permissions tab and change the Folder Access drop-down menu for Others so that it reads None. Then click the Apply permissions to enclosed files to ensure that they are locked down. Once you’ve done this, click the Close button to make sure that your home directory is protected from the snooping eyes of other users local to your machine.

# Step by step: Configure a firewall

![](bbox=[0.1, 0.39, 0.475, 0.58])

![](bbox=[0.515, 0.39, 0.89, 0.58])

1 After a brief introductory screen, you should click Forward to move to the Network Device setup. In the Detected Devices drop-down box, select the network interface that is connected to the internet – this is commonly eth0. If you know that your IP address is assigned dynamically by your internet router, then check the IP address is assigned by DHCP box. Click Forward to continue.

2 You’re probably using a router to connect to the internet, so you won’t need to enable connection sharing. However, if you are using your computer as the gateway to the internet, you should enable this setting and choose the network device that is connected to the local network. You can also choose to use DHCP to assign addresses dynamically to the local network, but you will need to have installed the dhcp3-server package prior to starting the Firestarter configuration.

![](bbox=[0.515, 0.68, 0.89, 0.88])

3 The final screen prompts you to save your options and start the firewall. If for some reason you don’t wish to start the firewall at this point, un-tick the Start Firewall Now check box and click the Save button.

# Password hacking

# How outsiders get your passwords

In Ubuntu, the user details are usually stored in /etc/passwd along with the numeric User ID and Group ID. The actual password is not stored here – instead you’ll see a small x when looking at this file, which denotes that there is a password present. The actual passwords are stored in an encrypted format within /etc/shadow, which will look like gibberish if you try to view it and will not resemble your true password. However, if an outsider manages to get a hold of this file then they can use a number of freely available tools to try to extract this password

information. Usually these tools rely on what are known as dictionary-based tools, in that they have a large collection of dictionary words that they use to try and unlock your password information. The tools will literally cycle through all the words available, as well as common misspellings, in an attempt to match one of them with your password. By using the technique that we showed you to create a strong password, you will minimise the risk of any dictionary-based attack as your password will not be based on a dictionary word.