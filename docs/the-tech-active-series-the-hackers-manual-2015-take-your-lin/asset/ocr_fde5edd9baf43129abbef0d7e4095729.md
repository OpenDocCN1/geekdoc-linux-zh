# # torrent server

you enter the web interface, Deluge will prompt you to change the password.

Before you can start using the web client you'll have to connect to the Deluge daemons. The web interface will automatically launch the Connection Manager window, which lists all of the running Deluge daemon. Simply select the daemon and click on the Connect button. You'll now be able to use the web client to add and control all your torrents running on the torrent box.

If you wish to change the port on which the web client runs, you'll need to edit its configuration file. Head to Deluge's configuration directory with `cd ~/.config/deluge/` and open the configuration file called `web.conf` in your favourite text editor. Scroll down the file and find the line that reads “port: 8112” and replace 8112 with any port number above 1000.

# ## Daemon's work

As mentioned earlier, to get the maximum out of Deluge you will need to configure the Deluge daemon to accept connections from a remote client. Start by pulling up the Deluge console client to make configuration changes to the Deluge daemon, with the command:

```
sudo apt-get install deluge-console
sudo pkill deluged
```

and open its configuration file `~/.config/deluge/auth` in your favourite text editor.

Scroll down to the bottom of the file and enter three parameters to specify the username and password you wish to use, along with the authentication level for the daemon, separated by a colon, such as `my-username:my-password:10`. Remember to replace the my-username and my-password parameters. The 10 authentication level gives the daemon administrative privileges.

Save the file and exit the text editor. Back at the console, start the Deluge daemon with the deluged command. Then head into the Deluge console by entering deluge-console in the terminal. This will launch the command-line interface for the Deluge daemon.

We'll use the console to make the Deluge daemon accept remote connections. In the console type:

```
config -s allow_remote True
```

The client will confirm that it has successfully changed the configuration value. You can now exit the console client by typing exit and then bring the changes into effect by first stopping the Deluge daemon with sudo pkill deluged and then starting it again with deluged.

That's all there's to it. Deluge is now all set up to accept connection from remote clients on the network. Follow the walkthrough to setup clients to connect to your box.

# ## Connect to the server

![](bbox=[0.075, 0.619, 0.939, 0.775])

+   1. **Install clients**
+      Now that the Deluge daemon is ready to accept connections, you'll need to install the Deluge desktop client on other computers on your network. Most desktop distributions include Deluge in their repositories so you can download it from the distro's package manager. Being cross-platform, you'll also be able to head to Deluge's download page to get Windows and Mac OS X clients, if needed.
+   
+   2. **Enable Classic mode**
+      By default, the Deluge clients are set up to download to the local computer. We want to change this behaviour, so you'll need to fire up the Deluge client and head to Edit > Preferences and switch to the Interfaces category. Here you'll notice a checkbox for Classic Mode which is enabled by default. Uncheck this box, click OK and then restart the Deluge desktop client.
+   
+   3. **Add host**
+      When you restart Deluge it will automatically fire up the Connection Manager. Click on the Add button in the Connection Manager and enter the connection details about the daemon. Click the Add button which takes you back to the Connection Manager. Select the added entry and click the Connect button to connect the client with the daemon running on the torrent box.

**Subscribe to Linux Format**  http://myfavouritemagazines.co.uk/LINsubs