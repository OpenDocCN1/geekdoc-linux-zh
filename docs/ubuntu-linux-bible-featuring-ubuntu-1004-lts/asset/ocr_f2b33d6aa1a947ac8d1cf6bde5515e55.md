If you are using a version of Ubuntu other than Linux Lynx (10.04), you should replace lucid with the name of the version of Ubuntu that you are using (karmic, jackalope, hardy, etc.). If you are using Synaptic, it will automatically update the lists of available packages that it knows about. If you directly modified your /etc/apt/sources.list file, you will need to tell whatever management software you are using to update its package lists. If you are using aptitude to install software, you can do this by executing the command sudo aptitude update from command-line environment. If you have problems updating package manager list of available packages, see Chapter 19 for more information about updating package lists in whatever package manager you are using.

Before installing Wicd, you should also import its privacy key so that your package manager won't warn you about the dangers of installing software from unauthorized sources. You can import this key from any command-line environment by executing the following command:

```
wget -q http://apt.wicd.net/wicd.gpg 0- | sudo apt-key add
```

After installing Wicd, you can use your favorite package management tool to install the wicd package. As a replacement for the Network Manager and its applets, Wicd conflicts with the Network Manager, and only one of these network connection packages can be installed on a system at a time. However, as mentioned previously, installing Wicd will automatically purge the Network Manager and related applets for you. Installing Wicd will automatically purge the Wicd daemon and install both the Wicd daemon (/usr/bin/wicd) and a Python-based client application for your Ubuntu system's Notification Area. This client application will start automatically the next time that you log in your system, but if it doesn't start automatically when you install Wicd, you can execute it manually by executing the command /usr/bin/wicd-client& from any command-line environment.

# Using Wicd

To start the client portion of Wicd, click on its tray icon to display a screen like the one shown in Figure 22-1.

This initial dialog should show an entry for the wired connection on your system and any wireless networks that have been detected. The wireless networks that are listed depend on those that are detected in your location—if the screen that you see when you first start Wicd looks exactly like the one shown in Figure 22-1, then I'm flattered (and a little creeped out) that you're reading this book from somewhere in my.

As you can see Figure 22-1, Wicd initially identifies all available wired and wireless connections, but does not automatically connect to any of them by default. To connect to any of them, click the Connect button below that entry. If you attempt to connect to a network that requires authentication, you will immediately see a dialog like the one shown in Figure 22-2, which tells you that the connection requires encryption.