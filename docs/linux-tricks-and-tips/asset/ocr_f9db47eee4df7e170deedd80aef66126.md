# How to Set Up Python in Linux

![](bbox=[0.86, 0.04, 0.92, 0.08])

However, if you want the latest, cutting edge version, you need to build Python from source. Start by entering these commands into the Terminal:

# STEP 5

```
sudo apt-get install build-essential checkinstall
sudo apt-get install libssl-dev liblz2-dev
libncurses5-dev libssl-dev libgdbm libsqlite3-dev tk-dev
libtcl-dev-dev libbz2-dev libg2z2-dev
```

![](bbox=[0.08, 0.24, 0.48, 0.38])

# STEP 6

Open up your Linux web browser and go to the Python download page: www.python.org/downloads. Click on Downloads followed by the button under the Python Source window. This opens a download dialogue box; choose a location and start the download process.

![](bbox=[0.08, 0.49, 0.48, 0.66])

# STEP 7

In the Terminal, go the Downloads folder by entering cd Downloads/. Then unzip the contents of the downloaded Python source code with tar -xvf Python-3.Y.Y.tar.xz replacing the Y's with the version numbers you've downloaded. Now enter the newly unzipped folder with cd Python-3.Y.Y/.

![](bbox=[0.08, 0.78, 0.48, 0.92])

# STEP 8

Within the Python folder, enter:

```
./configure
sudo make altinstall
```

This could take a while depending on the speed of your computer. Once finished, enter python3.7 --version to check the installed latest version. You now have Python 3.7 installed, alongside older Python 3.x.x and Python 2.

![](bbox=[0.54, 0.24, 0.93, 0.38])

# STEP 9

For the GUI IDLE, you need to enter the following command into the Terminal:

```
sudo apt-get install idle3
```

The IDLE can then be started with the command idle3. Note that IDLE runs a different version from the one you installed from source.

![](bbox=[0.54, 0.5, 0.93, 0.66])

# STEP 10

You also need PIP (Pip Installs Packages) which is a tool to help you install more modules and extras.

Enter: sudo apt-get install python3-pip

When PIP is installed, check for the latest update with: pip3 install --upgrade pip

When complete, close the Terminal and Python 3.x will be available via the Programming section in your distro's menu.

![](bbox=[0.54, 0.8, 0.93, 0.92])