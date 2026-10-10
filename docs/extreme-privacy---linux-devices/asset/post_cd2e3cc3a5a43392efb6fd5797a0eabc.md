
## All Ubuntu Installations:

- Select "Normal Installation", "Download Updates", and "Install third …".
- Click "Continue".
- Select "Erase disk and install Ubuntu", then "Install Now".
- Confirm with "Continue".
- Choose your desired time zone and click "Continue".
- Enter a desired name, username, computer name, and password for each field.
- Choose "Log in automatically" and click "Continue".
- Allow Ubuntu to complete the installation and choose "Restart Now".
- Click the "CD" icon in the upper-right of the UTM VM window; highlight the CD/DVD option, and click "Eject". THEN press "Enter" to restart the VM or the "left triangle" within UTM.
- If necessary, choose the "power" or "restart" icons in the UTM window.

Your device should now boot to the login screen. If it boots into the installation ISO again, shut the machine down. In the main UTM window, select your new machine and click the settings icon in the upper-right. Under "Drives", identify the CD/DVD drive and change "Image Type" to "None". Reboot the VM and boot into the Ubuntu Desktop. The following will finish the default configuration.

- Click "Skip" then "Next".
- Select "No" and then "Next" when asked to help improve Ubuntu.
- Click "Next" then "Done" to remove the welcome screen.
- If prompted to install updates, click "Remind me later".
- Continue to the section titled "Ubuntu Customization".

## Ubuntu Customization

You should now have an Ubuntu virtual machine executed within your Intel or ARM macOS device. Unlike the steps with VirtualBox, UTM does not require any special extension packs or software to be installed within the VM for the display to resize. You should be able to adjust your screen as desired, or make it full screen for best view. However, do not enter full-screen mode just yet. We still have some work to do and I want you to have easy access to the menu bar. Remember to always use the highest resolution available within Ubuntu and then choose the 100%, 200%, or additional options present within the Ubuntu display preferences. You can right-click the Ubuntu desktop and choose "Display Settings" to see this menu. Also, there are no concerning license restrictions. This is a much better scenario for all of us.

Some desired capabilities, such as clipboard and file sharing, require the installation of UTM’s Spice daemon. Launch Terminal from the Applications menu within Ubuntu, and execute the following, which will also modify our background to match the previous tutorial. You may already have the required software, but let’s make sure.

```
sudo apt install spice-vdagent spice-webdavd
gsettings set org.gnome.desktop.background picture-uri ''
gsettings set org.gnome.desktop.background primary-color 'rgb(66, 81, 100)'
```

Copy and paste capabilities should now be working, or you may not see your shared folder within Files on Ubuntu. The following should fix this.

- Shut down the VM and close the window.
- Within the main UTM window, click the "Settings" icon in the upper-right.
- Select "Sharing" on the left.
- Change "Directory Share Mode" to "Spice WebDAV" and click "Save".
- Reboot the VM.
- Click the "Shared folder" icon in the upper right of the UTM Ubuntu VM.
- Confirm your desired shared folder location.
- Open the Files application within Ubuntu.
- Click the "Other Locations" option in the left menu.
- Click the folder titled "Spice client" and wait for your VM to recognize it.
- Confirm you can access the shared folder within the left menu of Files.

It can take several minutes for the share to become available to Ubuntu. Once it does, it should appear until the VM reboots. Whenever you need to access the shared folder, simply click the Spice folder under "Other Locations" for that session. You can now copy files from your VM directly to your host and vice versa. I typically only do this after the VM has been booted for a while and I need the shared folder. Next, we should consider privacy and security settings within Ubuntu. The first two Terminal commands disable Ubuntu's crash reporting and usage statistics while the remaining steps within Ubuntu's operating system harden our overall privacy and security.

```
sudo apt purge -y apport apport-symptoms ubuntu-report
sudo apt autoremove -y
```

- Launch "Settings" from the Applications Menu.
- Click "Notifications" and disable both options.
- Click the "Privacy" option, then click "Screen" and disable all options.
- Click "File History & Trash", then disable any options.
- Click "Diagnostics", then change to "Never".
- Click the back arrow and click "Power", changing "Blank Screen" to "Never".
- Click "Automatic Suspend" and disable the feature.
- Close all Settings windows.

It is important to keep the software on this VM updated. There are different ways to do this, but I will focus on the easiest way within the operating system applications. While we do this, it may be a good time to add some commonly used applications to our Dock. Conduct the following steps.

- Launch the Applications menu (nine dots in lower-left).
- Type Terminal into the search field.
- Right-click on the application and select "Add to Favorites".
- Type Software into the search field and right-click on "Software Updater".
- Select "Add to Favorites".
- Press escape until all windows are gone.
- Launch the Software Updater icon from the Dock; click "Install Now"; and update all options.

UTM offers simple USB device access. While any USB drive is attached to the host computer, select the "USB Devices" icon in the upper-right of the UTM VM window. This presents that drive within the dock of Ubuntu for file transfer. If you plug in a USB device while the VM is running, it should prompt you to choose it. While a VM is shut down and the VM window is closed, you will see options within the main UTM application for the selected VM in the upper-right. We will focus on the "Clone selected VM" and "Share" menu options. Clicking the clone option simply presents an option to make a full clone. This allows us to preserve our original VM and make copies whenever we want. The share option allows us to export an entire VM within a ".utm" file for easy archiving or sharing. The dialogue will prompt you to choose the export location. If you ever want to see the location of all VMs within UTM, navigate to the following directory within the macOS host.

`/Users/[your macOS username]/Library/Containers/UTM/Data/Documents/`

If this location is not convenient, and I believe it is not, you can move your VM to any folder desired with the "Move selected VM" option within the main windows. I keep all of mine within a dedicated folder on my macOS host. Note that you can only move them once using the button option.

### Creating a Linux VM on a Linux Host

In the first section of this chapter, I explained the usage of VirtualBox to create a Linux virtual machine within a Windows system. Those instructions could also apply to using VirtualBox to create a Linux VM on a Linux host. However, I believe there is something better. QuickEMU (https://github.com/quickemu-project/quickemu) offers pre-built VMs which require little effort. Install the software and interface with the following commands.

```bash
sudo add-apt-repository ppa:flexiondotorg/quickemu -y
sudo add-apt-repository ppa:yannick-nauray/quickgui -y
sudo apt update
sudo apt install quickemu -y
sudo apt install quickgui
```

After installation, open the QuickGUI application and conduct the following.

- Click "Create new machines" and click the "Select" button.
- Search "pop" and select "Pop!_OS".
- Click "Version" and select the latest option, such as "22.04".
- Select the "Intel" option and click the "Download" button.
- Allow the download to complete and click the "Dismiss" button.
- Close the "Downloader" menu with the "X" in the upper-left.

You can now click the "Manage existing machines" button to access your VM(s) at any time. Click the play button (right arrow) next to any machine to launch it. Use the full-screen button to maximize your VM. Repeat the previous tutorials in order to replicate the Pop!_OS machine throughout this book. You can also easily experiment with over 300 different Linux builds within this software.

QuickEMU offers a macOS installation option, but I have found it unreliable. The Android option works, but the version is 9.0 and quite outdated. We will use something better soon.

### Creating a Windows VM on a Linux Host

For Linux hosts which need to possess Microsoft Windows, I recommend VirtualBox (virtualbox.org). This allows you to launch Windows applications whenever needed. VirtualBox installation instructions for Linux is as follows within Terminal.

```bash
sudo apt update
sudo apt install virtualbox virtualbox-ext-pack -y
```

Next, you need a copy of the Windows 11 installation media. I prefer the "Windows 11 (multi-edition ISO for x64 devices)" under the "Disk Image" section at https://www.microsoft.com/software-download/windows11. After download, launch VirtualBox and conduct the following.

- Click the "New" button.
- Provide a name of "Windows 11" and confirm your desired location.
- Select the downloaded ISO file and choose your desired edition.
- Confirm "Microsoft Windows" as type and "Windows 11 (64-bit)" as version.
