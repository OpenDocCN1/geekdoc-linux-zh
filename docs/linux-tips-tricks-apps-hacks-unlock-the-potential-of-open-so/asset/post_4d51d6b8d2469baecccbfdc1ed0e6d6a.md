
## BUILD A WEB SERVER

Host your web services on a dedicated server that you control

- **01 Install Apache**

Once you've got your server set up and can SSH in, it's time to install the Apache web server. Do that using the following:

```shell
$ sudo apt-get install apache2
```

It will automatically set the domain address to the following: 127.0.0.1

![](img/30dc0459712b32ede1a3814d456b41b6_23_0.png)

Above Give your web server a test once you've installed Apache

> “With a web server you can now use it to host your own website or to access storage from the server remotely over the Internet”

- **02 Test server**

If you have to install a GUI onto your server, you can test out that Apache is working by going to a browser in it and navigating to 127.0.0.1. Otherwise, from an external system, navigate to the IP address of your system in your browser and it should show the Apache confirmation page on-screen.

- **03 Install FTP**

With a web server you can now use it to host a website or to access storage from the server remotely over the Internet. You can set up the latter using FTP, or in our case the secure VSFTP. Install it to the system using:

```shell
$ sudo apt-get install vsftpd
```

- **04 Configure FTP**

We can access the configuration file for FTP by using nano to open /etc/vsftpd.conf (sudo nano /etc/vsftpd.conf). From here we can configure it to match our uses, but first it is necessary that we increase the security just slightly before using it properly as an FTP server, just to be on the safe side.

- **05 Secure your FTP**

The main change to make the FTP secure is to turn off anonymous users. In the config file, look for the line with 'anonymous_enable'. We want to change this to NO if it's not already there, just to make sure that there is a bit more security for the FTP server and that all of your content is kept private.

## EXPAND YOUR WEB SERVER

Tailor your web server to suit all of your individual needs

![](img/30dc0459712b32ede1a3814d456b41b6_24_0.png)

### Mail server

Part of the benefits of this being a web server is that it enables you to also add your own mail server to it, or even host your own webmail client as well. Having Apache configured is the first step to this, and it is quite straightforward to then set up a mail server on top of that.

As for a webmail client, we recommend using RainLoop, which looks nice and modern and also lets you add other webmail services to it, along with your own webmail server.

![](img/30dc0459712b32ede1a3814d456b41b6_24_1.png)

### Nginx server

Instead of using Apache for the server, you can also look into and try out Nginx. Nginx handles processes slightly differently than Apache and can result in a lighter load on your web server. It’s available in the repos of most distros, much like Apache is, so it can be installed in mostly the same way.

For a more complete guide to setting up an Nginx server, you can always refer back to one of our tutorials from *Mithals* – it’s inside issue 144, if you have it to hand, and on our website: bit.ly/1AYKx88.

![](img/30dc0459712b32ede1a3814d456b41b6_24_2.png)

- **06 Local use**
While it will be great to access these files externally, we might as well have it so you can access the FTP internally too, just in case you prefer that to a shared folder. Find the line ‘local_enable’ and change it to YES to make sure it’s accessible elsewhere.

- **07 Edit files**
As we are only letting people we want onto the server, we can make it so anyone logged in has write access. To do this, go back into the config file, look for the line with ‘write_enable’ and change it to YES. You may also need to uncomment it by removing the hash.

- **08 FTP Folder**
If you didn’t create a shared folder for the previous server tutorial, now is a good time to create a dedicated directory for this. In the home folder, use mkdir to create a directory called whatever you wish for the FTP server to be able to access it.

![](img/30dc0459712b32ede1a3814d456b41b6_24_3.png)

- **09 Restart server**
Once the config file has been fully edited and the folder is created, it is now time to start using it. Restart the FTP server using **sudo service vsftpd restart** and you will start to be able to access the folder. Any changes that you make to the configuration will require this restart to become active.

## SET UP LVM FILESYSTEMS

Understand the limitations of graphical partitioning when dealing with LVM filesystems

Create, name and modify logical volumes and volume groups that contain all your data

Add more hard drives and partitions to the LVM to keep expanding the space forever by allocating it smartly

![](img/30dc0459712b32ede1a3814d456b41b6_25_0.png)

Quite a different filesystem to your normal ext partitions, but LVM might just be the way to go

### Resources

- LVM 2 tools: [sourceware.org/lvm2](sourceware.org/lvm2)
- gparted: [gparted.org](gparted.org)

You'd be forgiven for not knowing what LVM stands for, but it's a useful thing to know. Logical volume management, as it's properly designated, acts as a sort of container to manage your data – the benefit of this is that you can start adding and extending space while the LVM is still online and working. This is great for server farms because you can swap out and add storage very quickly, and on your desktop its particularly good for managing the size of different partitions if you weren't sure how they should have been during installation.

In this tutorial, we'll look at how you can create an LVM filesystem and then how you can go about maintaining and modifying it. We will also look into how some distros install using LVM.

![](img/30dc0459712b32ede1a3814d456b41b6_26_0.png)

- **01 Install LVM**

Many distros have the option to install using an LVM filesystem. In our example, we've left the LVM option checked when installing Fedora 21. This will automatically create a boot and storage partition within the logical volumes for you to play about with later.

![](img/30dc0459712b32ede1a3814d456b41b6_26_1.png)

> “You can swap out and add storage very quickly, and on your desktop its particularly good for managing the size of different partitions”

- **02 Graphical partition editors**

General partition editors like gparted have a bit of a tough time working with LVM filesystems – with the right tools installed you can see the partition but you can't really do much to it. For this tutorial, we will be working mostly within the terminal.

![](img/30dc0459712b32ede1a3814d456b41b6_26_2.png)

- **03 Use LVM tools**

Although you can edit partitions live, we suggest booting into a live disc or other distro on the system instead. Once you have, install the LVM2 tools if they haven't been installed already. The package is called lvm2 in the repos and contains various tools for looking at, and manipulating LVM partitions, which is useful.

- **04 View the LV**

Now the tools are installed, we can have a peek at the LVs (logical volumes) on the system. This will display the volume group, the name type and size. Open up the terminal and use:

`$ sudo lvdisplay`

- **05 See the volume group**

The LVM partitions are kept inside a volume group, which in our case is called Fedora but could be called anything. You can get more accurate details on this by using the volume group tools like so:

`$ sudo vgs`

Tips | Tricks | Hacks | Apps

![](img/30dc0459712b32ede1a3814d456b41b6_27_0.png)

> “Make sure you know the designation of the partition”

- **06 Create an LVM**

It takes multiple steps to make an LVM filesystem. You need to create a physical volume for the volume group to be in and then you can create your logical volume inside that. First though, create a new partition on the system in your preferred method.

Make sure you still remember the partition designation and create it with something like:

```
$ sudo vgcreate LVDG /dev/sda3
```

You can add several partitions and/or hard drives like this as well.

- **07 Make a physical volume**

Once the partition is made, you can turn it into a physical volume. Make sure you know the designation of the partition (in our case /dev/sda3), which you can find out with `fdisk -l`. Create the PV with:

```
$ sudo pvcreate /dev/sda3
```

- **08 Include a volume group**

Now with a physical volume to play with, we need to create a volume group with a name.

- **09 Create a logical volume**

The final step is to include a logical volume. Give it a name, tell it how much space to use and which volume group it should belong in. To fill up a 20 GB volume group, use:

```
$ sudo lvcreate --name root --size 20G LVDG
```

- **10 Extend the volume group**

If you want to extend the space in your original volume group, first create a new physical volume as before. Find out the name of the volume group (**vgdisplay**) and use the designation of the partition to extend with:

```
$ sudo vgextend /dev/fedora /dev/sda3
```

- **11 Alter the logical volume**

Ensure that you know exactly how much space you have to extend the partition by using **vgdisplay** to find the free PE (physical extent) value, and also make sure you know the name of the partition that you are extending. Once you have both of those, then use:

```
$ sudo lvextend -L +4958 /dev/fedora/root
```

- **12 Resize the file system**

To finish off the extension, we need to let the entire LVM system know that it has had some changes using the resize option on the LV you’ve extended. The good thing is, this means you don’t need to have space “next to it” in the hard drive to extend in this way. Do this with:

```
$ sudo resize2fs /dev/fedora/root
```
