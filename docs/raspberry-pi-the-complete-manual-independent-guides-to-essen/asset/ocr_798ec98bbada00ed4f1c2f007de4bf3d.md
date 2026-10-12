# What you'll need... Rapsbian www.raspberrypi.org/downloads Internet connection

Did you know... You can network with other Linux, Windows and Mac OS X computers with Samba – it's totally cross-platform.

# Share your files with Samba

# Share your files with Samba

Configure your Pi to share the contents of the home folder over your home network

Regardless of whether you plan to set your Raspberry Pi up as a media centre, gaming machine or full-on development platform, the ability to share and access the contents of your Pi from other machines is very useful.

While the Raspberry Pi is very well configured, by default it doesn't include the ability to share the contents of your home folder with your local network. As you'll see from this guide, though, it's not too difficult to accomplish thanks to Samba and can help you access your scripts, media or documents from any other machine.

![](bbox=[0.05, 0.43, 0.32, 0.49])

# Update & install Samba

Open a terminal window and type the following into the terminal to update the Raspbian repository and then install Samba

```
sudo apt-get update && sudo apt-get install samba samba-common-bin
```

The operation itself shouldn't take too long. Just make sure that you're connected to the internet before you start

# Load smbc.conf

With the core packages installed, you now need to tell Samba how you want it to work. You do this by putting your preferred settings in Samba's configuration file. This file is called smbc.conf and it's located in the /etc/samba folder. While it's easy to locate it using the file managers, it's easier to open and edit it from the command line. Type the following into the terminal window to open it with nano:

```
1 sudo nano /etc/samba/smb.conf
```

# Initial setup

Take a look through the file. There's lots of information here and it seems a bit daunting, but there are only a handful of changes and additions to make. Firstly, you need to make sure you have assigned the correct workgroup. Unless your network has been configured differently, it will likely be called WORKGROUP. To find the workgroup setting, press Ctrl+W and type workgroup, then press Enter – this will take you to the first occurrence of the word 'workgroup'. Use the arrow keys to move between lines – the mouse doesn't work in nano.

![](bbox=[0.05, 0.7, 0.29, 0.91])

# Windows support

If you have Windows computers in your network, you'll need to ensure WINS support is allowed. Assuming you're working from the default smbc.conf configuration file, you'll find the flag for WINS support a few lines below the workgroup line. Edit it so it looks like this:

```
wins support = yes
```