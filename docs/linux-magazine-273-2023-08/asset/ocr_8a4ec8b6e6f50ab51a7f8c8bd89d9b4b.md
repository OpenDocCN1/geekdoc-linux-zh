# **Listing 2: Modifying Redis Parameters**

```
01 REDIS = {
02 	'tasks' : {
03 		'HOST': 'localhost',		# Redis server
04 		'PORT': 6379,				# Redis port
05 		'PASSWORD': '',		# Redis password (optional)
06 		'DATABASE': 0,			# Database ID
07 		'SSL': False,			# Use SSL (cahining)
08 	},
09 	'caching' : {
10 		'HOST': 'localhost',
11 		'PORT': 6379,
12 		'PASSWORD': '',
13 		'DATABASE': 1,			# Unique ID for second database
14 		'SSL': False,
15 	}
16 }
```

If you are also installing this on Ubuntu Desktop, use:

```
$ sudo gedit configuration.py
```

For versions of Ubuntu newer than 20.04, use:

```
$ sudo gnome-text-editor configuration.py
```

You will then be able to edit the file directly in a text editor. This might be easier if you are less familiar with using Vim or nano from the terminal.

You will need to modify four keys in the config file (Figure 4). First, you will change the ALLOWED_HOSTS parameter:

```
ALLOWED_HOSTS = ['netbox.example.com',
 '192.168.2.13']
```

If you unsure about what to enter here, use your server’s IP address, which you can get by typing

```
$ ip addr
```

ess into the terminal. You can also type `$` hostname into the terminal and put your server’s hostname here as well, or you can use both if that makes sense. My installation has four entries here, separated by commas. You will enter this in a web browser later to get to the NetBox web GUI.

Warning: Do not type this in the example ALLOWED_HOSTS comment directly above the ALLOWED_HOSTS parameter. If you get a 400 bad request error, I suggest checking the ALLOWED_HOSTS comment to see if you accidentally entered your IP address or hostname there.

Next you need to modify the database parameters as shown in Listing 1.

You then need to modify the Redis parameters as shown in Listing 2.

Finally, you will need to modify the secret key parameter. First, you need to generate your secret key with:

```
$ python3 /opt/netbox/netbox/
	generate_secret_key.py
```

Copy and paste the generated key into the SECRET_KEY parameter space below the REDIS parameter. You will use this key if you decide to set up a second NetBox server for backup, so jot it down for future reference. If you forget to do this, you can always get back into configuration.py to retrieve the secret key if needed later.

Now you can create and edit the local_requirements.txt file with:

```
$ cd /opt/netbox/
$ sudo nano local_requirements.txt
```

If you intend to use a remote database as mentioned in the online documentation, you will want to enter djangostorages [12] here. What is not clear in the documentation is that you also need to enter any other plugins that you intend to use in the local_requirements.txt file in /opt/netbox. (For a list of NetBox plugins, see the NetBox Community Plugins GitHub page [13].) In addition, the plugins need to be listed in the previously modified configuration.py file in /opt/netbox/netbox/netbox.

In local_requirements.txt, simply enter each desired plugin (Figure 5), one per line, as follows:

+   djangostorages
+   netbox-topology-views
+   netbox-inventory
+   netbox-rqcode

In local_requirements.txt, note that the plugins use dashes (-). When you edit the configuration.py file, you will change some of the dashes to underscores (_). I found this super frustrating and inconsistent because it is not always dashes in one place and underscores in the another, but it is often different between the two. (If you build plugins for NetBox and can avoid this, please consider making your plugin names one word to avoid this issue.)

Now that you have edited and saved the local_requirements.txt file to include your desired plugins, you also need to enable them by once again modifying the configuration.py file. You can open configuration.py with:

```
$ cd /opt/netbox/netbox/netbox/
$ sudo nano configuration.py
```

Look for the PLUGINS parameter and, depending on the plugin, you may also need to change PLUGINS_CONFIG as well. Based on the plugins I added to my local_requirements.txt file, my PLUGINS section should look like this:

![](bbox=[0.06, 0.82, 0.6, 0.94])