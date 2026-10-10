# How to Set Up Python in Linux

**STEP 5**
However, if you want the latest, cutting edge version, you need to build Python from source. Start by entering these commands into the Terminal:

```
$ sudo apt-get install build-essential checkinstall
$ sudo apt-get install tlibreadline-gplv2-dev
$ libcurses5-dev libssl-dev libsqlite3-dev tk-dev
$ libgdcm-dev libtcl-dev libbz2-dev
```

```
```
david@david-Mint:
$ sudo apt-get install build-essential checkinstall
Reading package lists... Done
Building dependency tree
Reading state information... Done
build-essential is already the newest version (12.4ubuntu3).
```
```

**STEP 6**
Open up your Linux web browser and go to the Python download page: [www.python.org/downloads](http://www.python.org/downloads). Click on Downloads followed by the Python under the Python Source window. This opens a download dialog box; choose a location and start the download process.

![](bbox=[0.07, 0.5, 0.47, 0.65])

**STEP 7**
In the Terminal, go to the Downloads folder by entering `cd Downloads`. Then unzip the contents of the downloaded Python source code with `tar -xvf Python-3.Y.Y.tar.xz` replacing the Y’s with the version numbers you downloaded. Now enter the newly unzipped folder with `cd Python-3.Y.Y`.

```
```
Python-3.2.5/Include/cconfig.h
Python-3.2.5/Include/cpython.h
Python-3.2.5/Include/Python.h
Python-3.2.5/Modules
Python-3.2.5/PC/ldconfig.py
Python-3.2.5/PC/pyconfig.h
Python-3.2.5/PC/pystring.x
Python-3.2.5/PC/pcbuild.py
Python-3.2.5/PC/pyconfig.h
Python-3.2.5/PC/pystring.x
```

```
david@david-Mint:~$ tar -xvf Python-3.7.2
david@david-Mint:~$ cd Python-3.7.2
```
```

**STEP 8**
Within the Python folder, enter:

```
./configure
$ sudo make install
```

This could take a while depending on the speed of your computer. Once finished, enter `python3.7 --version` to check the installed latest version. You now have Python 3.7 installed, alongside either Python 3.x.x and Python 2.

```
```
Checking whether compile and linking works... Yes
... Configuring C compilation suites...
... Configuring C++ compilation suites...
... Configuring configuration suites...
```

```
david@david-Mint:~/Downloads/Python-3.7.2 $ sudo make install
```
```

**STEP 9**
For the GUI IDLE, you need to enter the following command into the Terminal:

```
$ sudo apt-get install idle3
```

The IDLE can then be started with the command `idle3`. Note that IDLE runs a different version from the one you installed from source.

```
```
david@david-Mint:~$ sudo apt-get install idle3
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following additional packages will be installed:
  Python idlelib
The following NEW packages will be installed:
  Python idle3
0 to upgrade, 2 to newly install, 0 to remove and 3 not to upgrade.
Need to get 524 kB of archives.
After this operation, 1.421 MB of additional disk space will be used.
Do you want to continue? [Y/n] Y
```
```

**STEP 10**
You also need PIP (Pip Installs Packages) which is a tool to help you install more modules and extras. Enter `sudo apt-get install python3-pip`

When PIP is installed, check for the latest update with:

```
pip3 install --upgrade pip
```

When complete, use the Terminal and Python 3.x will be available via the Programming section in your desktop’s menu.

```
```
david@david-Mint:~/Desktop/Python-3.7.2 $ sudo apt-get install python3-pip
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following additional packages will be installed:
  Python idlelib
The following NEW packages will be installed:
  Python idle3
0 to upgrade, 2 to newly install, 0 to remove and 3 not to upgrade.
Need to get 1.386 kB of archives.
After this operation, 2.501 MB of additional disk space will be used.
Do you want to continue? [Y/n] Y
```
```