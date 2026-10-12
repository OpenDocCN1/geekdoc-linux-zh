# Share your files with Samba

Projects

![](bbox=[0.08, 0.1, 0.93, 0.64])

# Add your share

**05** Next you need to find the section of the file called Share Definitions. Again, you can use the key combination Ctrl+W to open the search function, then type ‘share definitions’ and press Enter to be taken directly to it— it’s located right towards the end of the document.

Go to the very end of the document and add the following.

```
```​
[pi]
path=/home/pi
only guest = no
browseable = yes
writable = yes
```
```

# Set up passwords

```
```​
create mask = 0777
director mask = 0777
public = no
```
```

**06** You have finished editing the /samba.conf file now. So, to save and exit, press Ctrl-X, then press Y to save, and Enter to exit.

With this configuration, a layer of password security is in place, so we now need to set up a Samba password to use with it. In your terminal window, type the following command:

```
`smbpasswd -a pi`
```

You’ll be prompted to enter and confirm a new password. This is now your username and password for accessing your files.

# Restart Samba

**07** The final step is simply to restart Samba for your new settings to take effect.

At the terminal, type the following command to do so

```
`sudo /etc/init.d/samba restart`
```

The next time you look at your home network from another machine, you’ll see your Raspberry Pi’s home folder listed as a share