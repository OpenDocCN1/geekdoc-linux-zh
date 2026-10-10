# Install Guest Additions

So your VM can use USB devices and other system tools you need to install VBox Guest additions into the Kali VM (Make sure you have updated like above before starting this) There are no optional steps so make sure you can do them successfully before moving on.

To check for linux headers you are looking for the current linux-headers that end in – kali-all-amd64 the version will change over time.

![](bbox=[0.14, 0.34, 0.85, 0.42])

This will generate a list (if\u updated correctly) when you type in apt-cache search header \| grep -i linux look for the one ending in –kali-all-amd64

![](bbox=[0.14, 0.53, 0.85, 0.65])

![](bbox=[0.14, 0.66, 0.85, 0.72])

Install Linux headers at the time of writing it went to 4.5 this does change so type in the version you see when you do the apt-cache search header \| grep -I linux and install with **apt-get install linux-headers-4.5.0-kali-all-amd64**

When that finishes (just in case) run **apt-get update && apt-get upgrade -y** (there might be nothing to update but it is good to check) then in the terminal type **reboot**