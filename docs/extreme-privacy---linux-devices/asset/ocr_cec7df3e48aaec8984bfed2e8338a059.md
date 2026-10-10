# ## VLC

Pop!_OS does not include any powerful media player. If you will ever encounter various audio and video files, I highly recommend installing VLC from Pop!_Shop.

# ## Office

Pop!_OS includes the LibreOffice suite of applications for word processing, spreadsheets, and presentations. However, I prefer ONLYOFFICE for this purpose. It can safely be installed from Pop!_Shop.

# ## BleachBit Cleaner

After some time, your Linux device will likely become saturated with old cache files, leftover data, and other unnecessary files. I recommend executing BleachBit once weekly to keep things under control. I prefer the BleachBit (as root) option within the Pop!_Shop (Flatpak). I accept the default configuration upon first launch. I then select every option except "Free Disk Space" and click "Clean". At this point in the book, while working from a new machine, I was able to free 1.02 GB of data.

# ## Utilities

I prefer to add a few system utilities to any Linux distribution including GNOME Feeds for RSS, GNOME Podcasts for podcasts, and Metadata Cleaner to sanitize personal information from within files. All of these can be installed from within the Pop!_Shop with the default options. For Metadata Cleaner to function, you also need a utility called mat2, which can be installed via Terminal with the following.

```
sudo apt install mat2 -y
```

After a reboot, you can right-click on any image, video, or other file which may contain hidden metadata and clean the content. This will produce a second file next to the original with "clean" added to the file name.

# ## Virtual Currencies

If you need virtual currency access, I always recommend an offline software-based wallet without the need for a third-party exchange. I rely on Electrum for Bitcoin and Monero GUI Wallet for Monero. While you may find these programs within Pop!_Shop or another software repository, I would only install them directly from their original source. I obtain the AppImage file from the official Electrum site located at https://electrum.org/#download and then right-click the file to install it with AppImageLauncher. I then download the compressed Linux 64-bit file from the official site at https://web.getmonero.org/downloads, decompress it, and then right-click the Monero AppImage file to finish the installation process.

# ## Application Updates

You should keep your newly-installed software updated. The "Installed" tab within Pop!_Shop will allow you to patch your operating system and any Flatpak/Deb programs, but it does not update all individual applications. I keep the following commands digitally ready within my local notes application for easy copying and pasting, but a future chapter will present a custom script which will automatically execute all of these commands.

```
sudo apt update
sudo apt upgrade -y
sudo apt full-upgrade -y
pop-upgrade release upgrade
sudo apt autoremove -y
sudo apt autoclean -y
flatpak update -y
```