```
```
|| / Name Version Description
++==========================
ii bash 3.1-2ubuntu6 The GNU Bourne Again SHEll
```
```

# ## What Is That Strange File?

Let's say that you are wondering what some file is doing on your system. For instance, there is something called pinwrapper in my `/usr/bin` directory and I don't remember installing it. Furthermore, if I try to look it up in the man pages, I am told that there is no information on this file. Using the `-S` flag, I can have `dpkg` identify what package this file was a part of:

```
```
dpkg -S /usr/bin/pinwrapper
bluez-utils: /usr/bin/pinwrapper
```
```

Even though I don't remember installing this `bluez-utils` software, I can now use `apt-cache` `show` `bluez-utils` to tell me what this package is for. As it turns out, they are tools for using Bluetooth devices.

# ## Using apt-get to Install or Update Software

People who use Debian distributions on a regular basis sometimes point to this wonderful little program as the reason why Debian is so great. Well, I certainly won't be the one to deny that `apt-get` is wonderful.

If you want to install a package called `txttype` (a great typing tutor for kids, by the way), this is how to do it:

```
```
sudo apt-get install txttype
Reading package lists... Done
Building dependency tree... Done
The following extra packages will be installed:
  libssl-image1.2 libssl-mixer1.2
The following NEW packages will be installed
  libssl-image1.2 libssl-mixer1.2 txttype
0 upgraded, 3 newly installed, 0 to remove and 1 not
upgraded.
Need to get 4341kB of archives.
After unpacking 6038kB of additional disk space will be
used.
Do you want to continue [Y/n]?
```
```