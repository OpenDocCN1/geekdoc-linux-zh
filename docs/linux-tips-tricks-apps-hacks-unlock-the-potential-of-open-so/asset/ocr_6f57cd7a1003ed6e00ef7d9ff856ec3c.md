# "With just a desktop computer and SD card reader, there is a way that you can recover your password"

```
pi@raspberrypi:~$ sudo useradd -m aliciaokarma -G sudo
pi@raspberrypi:~$ sudo passwd aliciaokarma
Enter new UNIX password:
Retype new UNIX password:
passed: password updated successfully
Command "sudo passwd" completed. 
```

# **01 Stop using the default password**

Everyone who uses a Raspberry Pi knows that the default Raspberry credentials are 'pi' and 'raspberry'. Naturally, this means that anyone can sign into your computer if you haven't changed these defaults - something you'll need to do as a matter of urgency. After signing in, open the terminal and set a new password with:

```
password
```

![](bbox=[0.1, 0.45, 0.42, 0.6])

# **04 Give the new account a password**

With the new account set up, the next step is to set a password. As you're not signed into the account at this stage, you won't be using the `passwd` command. Instead, enter:

```
sudo passwd username
```

With the new account ready to use, you should be ready to remove the default pi account from Raspbian altogether.

![](bbox=[0.45, 0.53, 0.78, 0.64])

# **02 Change password with raspi-config**

If you're setting up a new installation of Raspbian, changing the password is one of the first things that you should do. With a new install, the first boot will automatically run the raspi-config screen. Here, use the arrow keys to find the second option, change User Password and then follow the on-screen prompts to set yourself a new password.

```
pi@raspberrypi:~$ sudo useradd -m aliciaokarma -G sudo
pi@raspberrypi:~$ sudo passwd aliciaokarma
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```

# **05 Delete the default Raspbian account**

You no longer need the default user account, so sign out and log in to your new account, and confirm it is correctly set up by opening:

```
sudo visudo
```

...and adding...

```
username ALL=(ALL) NOPASSWD: ALL
```

...to the final line. Save and exit with Ctrl+X. Now that's done, simply delete the old account with:

```
sudo deluser pi
sudo 'deluser --remove-home pi'
```

# **03 Create a new user account**

To completely baffle anyone attempting to gain access using default credentials, take the most secure option and create a new user account. In the command line, enter:

```
sudo useradd -m username -G sudo
```

The -m switch creates a new home directory, while the second sudo adds the new account to the superuser group.

# **06 Recover a lost password**

If you've somehow forgotten your Raspberry Pi user account password or suspect that someone has changed it, what can you do?

With a desktop computer and SD card reader, there is a way that you can recover your password. Begin by inserting the Pi's SD card into your PC's SD card reader.

![](bbox=[0.8, 0.51, 0.95, 0.89])