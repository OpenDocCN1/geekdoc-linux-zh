
+ Pop!_OS: Finally, we have my preferred operating system for myself and clients. Pop!_OS is based on Ubuntu, but redesigned for privacy and security. There are many differences from stock Ubuntu, including the following.
    - The Pop!_OS installer applies full-disk encryption by default.
    - All telemetry is disabled and third-party connections are opt-in.
    - The application store can install and update Flatpak/Deb programs.
    - Snap is not installed.
    - Pop!_OS has better window tiling options.
    - It includes a recovery partition to easily restore your system when needed.
    - It feels less sluggish and more polished.

While almost all of the remainder of this guide can be used with Ubuntu, Mint, or any other Debian-based distribution, I will focus on Pop!_OS within my demonstrations. Please do not let that deter you from testing other options. I had to choose one operating system for my examples, and I chose Pop!_OS because that is what I use every day. It should be quite easy to replicate all techniques within Ubuntu with minimal, if any, alterations. If you use Arch, Fedora, Manjaro, or another flavor of Linux, you know your reasons why, and should proceed with your own preference.

If you purchased a machine which included Pop!_OS, you can skip the next section. For those installing Pop!_OS (or any other version of Linux) themselves onto a dedicated host computer, you will need to create a bootable USB installation drive. I conducted the following to create my own drive.

- Navigate to https://pop.system76.com/ and click "Download".
- Choose the "Download 22.04 LTS" option and allow the download.
- Install Balena Etcher from https://etcher.balena.io/.
- Launch Balena Etcher and click "Flash from file".
- Select the downloaded iso file.
- Click "Select target" and choose your USB drive.
- Click "Flash" and allow the process to complete.

Please note that this will completely erase any chosen USB drive, so be careful. At the end of the process, you should have a bootable USB drive ready for Linux installation. Insert this drive into your computer and turn it on. Immediately press the key which presents boot options. This is typically, ESC, F1, F7, F8, F10, or DEL. Once you have your boot options screen loaded, select the USB drive with your Linux installation. The exact process to install any Linux distribution, including Pop!_OS, will change over time. However, the following steps used during the writing of this guide should help get you through the process. My experience with Pop!_OS is outlined in the following.

- Click "Try or Install Pop!_OS".
- Choose your desired language, location, and keyboard.
- Choose clean install and select your internal drive.
- Click "Erase and Install".
- Provide your desired computer name and password.
- Select the default option to encrypt the drive.
- If desired, allow the same Linux password to be used for the drive encryption. This is more convenient but could pose a security risk. If you want an extra layer of protection, you could specify a unique password for each option of drive encryption and Linux, but this may be overkill for most users. I use the same password for both options.
- Allow the process to complete and click "Restart Device".

When the computer reboots, you should be presented with a screen to unlock the encrypted disk with a password. This is the first layer of protection which comes default in Pop!_OS. This same protection can be configured during installation of Ubuntu or other systems. Unlocking the drive simply allows access to it. You should then be presented with the Pop!_OS user selection and password entry screen. This unlocks your version of Pop!_OS and boots the machine. Continue through the one-time setup with the following steps.

- Choose your layout options for the dock and click "Next".
- Choose your Top Bar options and click "Next".
- Click "Next" twice to continue through the menu.
- Choose your desired appearance and click "Next".
- Choose your Wi-Fi (if available), supply the password, and click "Next".
- Keep location services disabled and click "Next".
- Choose your desired time zone and click "Next".
- Click "Skip" to bypass any online accounts then click "Start Using Pop!_OS".

Some people are annoyed at the need to enter the same password twice upon each boot. I do not mind this, but I respect the question of redundancy. If you know the password to decrypt the drive, I do not see a huge security issue if you disable the secondary password to log into Pop!_OS. This can be done with the following steps, and reversed at any time, but please note my warning presented in a moment.

- Launch the Settings application in the lower-right of the dock.
- Choose "Users" in the left menu.
- Click "Unlock" and enter your password.
- Enable the "Automatic Login" toggle.
- Close Settings and reboot the computer by click the upper-right menu bar and selecting "Power Off / Log Out" > "Restart" > "Restart".

You should now only be prompted for the decryption password. Once past that screen, Pop!_OS should boot normally. **I want to stress that this is optional.** If you choose a unique password for each the decryption and login, you should not enable automatic login. This will also cause some programs to demand your password more often than if one was manually entered at login due to the way the Linux keyring is unlocked. Always identify the appropriate balance of convenience and security for your own needs. Enabling automatic login does not erase the password for the account, or decrease the security when a password is required otherwise, but it may add more inconvenience than if you just entered it at every boot, which is what I do.

Pop!_OS is more private than Ubuntu by default, but I still like to make a few modifications. I conduct the following after a new installation.

- Launch the Settings application in the lower-right of the dock.
- Click "Bluetooth" in the left menu and disable the toggle.
- Click "Privacy" in the left menu and disable "Connectivity Checking".
- Click "File History & Trash" and disable everything.

While the following are not related to privacy or security, I find the modifications to enhance my own usage of Linux. Your preferences may not match.

- Click "Screen" and change "Blank Screen Delay" to a longer period.
- Go back to the main screen, click "Power" in the left menu and disable "Automatic Screen Brightness" and "Dim Screen".
- Click "Automatic Suspend" and disable all options.
- Enable "Show Battery Percentage".

Much like Ubuntu, Pop!_OS offers numerous images for use as our background wallpaper. Right-clicking on the desktop presents a menu with an option to "Change Background". However, I prefer a solid background without any image. Similar to Ubuntu, Pop!_OS does not offer a menu option to change the background to a solid color. Let’s fix that. The following Terminal command removes the background image completely, leaving a solid blue background on the desktop. You can launch Terminal from the black icon in the lower Dock.

```
gsettings set org.gnome.desktop.background picture-uri ''
```

This is better, but I prefer a slightly muted version of blue, which I change with the following Terminal command. This command, and the others in this chapter, should be executed as a single command within one line. Your PDF viewer may split the lines and you will need to move everything within one command.

```
gsettings set org.gnome.desktop.background primary-color 'rgb(66, 81, 100)'
```

You can change the numbers as desired to create the perfect color for your desktop. The site at https://www.w3schools.com/colors/colors_rgb.asp should assist.

The next modification I like to execute is to move the Dock from the bottom to the left with the following Terminal command.

```
gsettings set org.gnome.shell.extensions.dash-to-dock dock-position LEFT
```

Next, I prefer to decrease the default size of the icons since I will be adding numerous programs soon. You can change the number to any size appropriate for your screen size with the following Terminal command.

```
gsettings set org.gnome.shell.extensions.dash-to-dock dash-max-icon-size 30
```

When you right-click a file or folder to delete it, you currently have the option to "Move to Trash". The following Terminal command adds a new option directly underneath the Trash entry titled "Delete Permanently". This allows me to bypass the Trash altogether and simply eliminate any desired content.

```
gsettings set org.gnome.nautilus.preferences show-delete-permanently true
```

By default, most Linux operating systems hide "hidden" files from view. These are typically system files but can also include cache and configuration files which we may need to access. Therefore, I execute the following two Terminal commands in order to make these valuable files visible at all times.

```
gsettings set org.gnome.nautilus.preferences show-hidden-files true
gsettings set org.gtk.Settings.FileChooser show-hidden true
```

You likely have pending operating system updates which should now be applied.

- Click the "Pop!_Shop" icon in the dock bar next to Settings.
- Click the "Installed" tab and then "Update All".

Once we begin installing applications, you will see additional update options within this menu. I typically launch Pop!_Shop at least once weekly to apply all updates.

While you may be tempted to begin installing all of your desired applications, please