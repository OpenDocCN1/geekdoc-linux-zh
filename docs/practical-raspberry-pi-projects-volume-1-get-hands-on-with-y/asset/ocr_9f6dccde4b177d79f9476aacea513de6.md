# TRANSFORM YOUR PI INTO A MICRO OSCILLOSCOPE

![](bbox=[0.12, 0.12, 0.79, 0.43])

**02 Open up the box**
Once you have received your BitScope Micro and opened up the box for the first time you should find all of the pictured items inside (if you get any extras, then it is obviously your lucky day). The main contents are the BitScope Micro itself (with mini USB cable preattached) and a set of ten test clip grabbers. There is also a variety of documentation containing a large amount of product info and guidance.

![](bbox=[0.45, 0.44, 0.79, 0.58])

**About The BitScope Micro comes complete with test clip grabbers and a whole lot of documentation**

**03 Update your Raspberry Pi**
As with almost every project you undertake on the Raspberry Pi, it pays dividends to make sure your operating system is updated to the latest stable version, as this can save a lot of hassle further down the line. To do this, open an LXTerminal session and then type:
$ sudo apt-get update
$ sudo apt-get upgrade -y
Then wait patiently for the upgrade process to complete.

![](bbox=[0.12, 0.69, 0.45, 0.85])

**04 Locate the BitScope Software**
Now your Raspberry Pi is all up to date you need to acquire the BitScope DSO (digital storage oscilloscope) software. This is not yet available as a Raspbian package, but it is very easy to install. Anyway using the downloadable DEB file. Visit [www.bit-scope.com](http://www.bit-scope.com) and click on the Download link at the top.

**05 Download the software**
The previous step should have brought you to the BitScope Downloads page. From here you need to download the top item in the list, BitScope DSO 2.7 (beta), and save it to the /home/pi directory on your Raspberry Pi so you know where to find it later. On some browsers the file will automatically download to the /home/pi/Downloads directory.

**06 Install the software**
Now we have downloaded the package, the easiest way to install the software is to open an LXTerminal session and then run the following code...
$ sudo dpkg -i bitscope-dso_2.7.EA17h_amhfd.deb
...or the equivalent version for newer software. You should see lines of output as the installation progresses. The BitScope DSO software then appears in the main menu under Other.

**07 Overclock your Raspberry Pi (optional)**
The BitScope software will run fine on a Raspberry Pi with default settings, however it can be a bit slow to respond. Open an LXTerminal session and type sudo raspi-config. In the menu, select option 7 Overclock. Click OK on the following screen and on the next one select Turbo. Click OK and then you should see some code run. Once this completes press Ok and then you are brought back to the main raspi-config window. Select Finish at the bottom right, and then select Yes to reboot your Raspberry Pi.

# Multiple platform support

One of the best things about the BitScope Micro (as well as its big brother, the BitScope BSM10) is that it's capable of running on a Pi and on any Linux, Windows or Mac OS X device with a USB port. The graphical UI is identical on each of these devices so it's easy to switch between them. The BitScope Micro should also work with smartphones capable of USB on-the-go connections, but there is no software available to take advantage of this yet.