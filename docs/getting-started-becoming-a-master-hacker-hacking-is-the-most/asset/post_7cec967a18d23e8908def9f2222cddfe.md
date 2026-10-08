
Then click **Start**.

Congratulations! You are on your way!

## Setting Up Kali

Kali will now open a screen like below, offering you several startup choices. I suggest using the graphical install for beginners.

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_112_0.png)

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_113_0.png)

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_114_0.png)

Use your keyboard keys to navigate the menu.

If you get an error when you’re installing Kali into your VirtualBox, it’s likely because you don’t have virtualization enabled within your system's BIOS. Each system and its BIOS will be slightly different, so check with your manufacturer or search online for solutions with your system and BIOS. In addition, on Windows systems, you will likely need to disable any competing virtualization software such as Hyper-V.

Again, an internet search for your system should guide you in doing so.

You will next be asked to select your language. Make certain you select the language you are most comfortable working in and then click **Continue**. Next, select your location, click **Continue**, and then select your keyboard layout.

When you click **Continue**, VirtualBox will go through a process of detecting your hardware and network adapters. Just wait patiently as it does so. Eventually, you will be greeted by a screen asking you to configure your network, like below.

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_115_0.png)

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_116_0.png)

The first item it asks for is the name of your host. You can name it anything you please, but I left mine with the default “Kali.”

Next, you will be asked for the domain name. It’s not necessary to enter anything here. Click **Continue**. The next screen is very important. Here, you are asked for the password you want to use for the *root* user.

The root user in Linux is the all-powerful system administrator (sysadmin). You can use anything you feel secure with. If this were a physical system that we are using on the Internet, I would suggest that you use a very long and complex password to limit the ability of an attacker cracking it. Since this is a virtual machine that people can’t access without accessing your host operating system, password authentication on this virtual machine is less important, but still, choose wisely.

Click **Continue**, and you will be asked to set your timezone. Do so and then continue.

The next screen asks about partition disks. Choose **Guided – use entire disk**, and Kali will detect your hard drives and set up a partitioner automatically.

Kali will then warn you that all data on the disk you select will be erased… but don’t worry! This is a virtual disk, and the disk is new and empty, so this won’t actually do anything. Click **Continue**.

Kali will now ask you if you want all files in one partition (a partition is just what it sounds like—a portion or segment of your hard drive) or if you want to have separate partitions. If this was a production system, you probably would select separate partitions for /home, /var, and /tmp, but considering that we will be using this as a learning system in a virtual environment, you should simply select **All files in one partition**.

Now you will be asked whether to write your changes to disk. Select **Finish Partitioning and write changes to disk**. Kali will prompt you once more to see if you want to write the changes to disk; select **Yes** and click **Continue**.

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_119_0.png)

Kali will now begin to install the operating system. This could take a while, so be patient. Now is the time to take your bathroom break and get your favorite beverage.

Once the installation is complete, you will be prompted as to whether you want to use a network mirror.

This really is not necessary, but you may want to select a network mirror updates and additional software near your physical location.

Then Kali will install GRUB (Grand Unified Bootloader). A bootloader enables you to select different operating systems to boot into, which means when you boot your machine you can boot into either Kali or another operating system. Select **Yes**. Then Kali will install the GRUB bootloader.

On the next screen, you will be prompted as to whether you want to install the GRUB bootloader automatically or manually. For reasons as yet unclear, if you choose the second option, Kali will tend to hang and display a blank screen after installation. Select **Enter Device Manually**.

On the following screen, select the drive where the GRUB bootloader should be installed (it will likely be something like */dev/sda*). *Unlike Windows, Linux designates hard drive as sda, sdb, etc. See Linux Basics for Hackers for more information*. Click through to the next screen, which should tell you that the installation is complete.

Congratulations! You installed Kali. Click **Continue**. Kali will attempt to reboot, and you will see a number of lines of code go across a blank, black screen before eventually **you are greeted with Kali 2019**‘s login screen, as shown below.

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_121_0.png)

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_121_1.png)

Login as *root*, and you will be asked for your password. Enter whatever password you selected for your root user.

After logging in as root using your password, you will be greeted with the Kali Linux desktop like that below.

## Installing Your Target Systems

Throughout this book, we will focus on two target systems, Metasploitable 2, a purposely vulnerable Linux system, and Windows 7. To download and install Metasploitable 2, go to [https://sourceforge.net/projects/metasploitable/](https://sourceforge.net/projects/metasploitable/). Once it has been downloaded, simply follow the instructions above for Kali to install your Metasploitable 2. The login for Metasploitable 2 is username: *msfadmin* and password: *msfadmin*.

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_122_0.png)

### Create Virtual Machine

**Name and operating system**

| Parameter | Value |
| :--- | :--- |
| Name | Windows 7 Target |
| Machine Folder | C:\Users\OTW\VirtualBox VMs |
| Type | Microsoft Windows |
| Version | Windows 7 (64-bit) |

**Memory size**

4 MB - 16384 MB
*Default*: 2048 MB

**Hard disk**

- Do not add a virtual hard disk
- Create a virtual hard disk now
- Use an existing virtual hard disk file

Kali 2019.vdi (Normal, 26.67 GB)

- Guided Mode
- Create
- Cancel

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_124_0.png)

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_124_1.png)

To install Windows 7, things are a bit trickier. For you to fully engage with our exercises on Windows 7, you will need an unpatched Windows 7 system. Maybe you have one around your home, school, or office.

If not, you can search around the Internet and find numerous downloadable copies. Install it into your VirtualBox system, just as you did with Kali above.

Eventually, you will be greeted by that familiar Windows 7 login screen.

Lastly, we need to install MySQL on to the Windows 7 system. Go to www.oldapps.com and search for Windows applications. Go to the MySQL server and download and install MySQL v5.5.1.

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_125_0.png)

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_126_0.png)

Once you have installed MySQL for Windows, you will need to open the MySQL terminal (go to **Programs** then **MySQL**) to create our test database and populate the database with the following commands.

```sql
CREATE DATABASE `moviedb`;
CREATE TABLE `creditcards` (
  `id` varchar(20) DEFAULT NULL,
  `first_name` varchar(50) DEFAULT NULL,
  `last_name` varchar(50) DEFAULT NULL,
  `expiration` date DEFAULT NULL
);
ALTER TABLE `creditcards` DISABLE KEYS;
INSERT INTO `creditcards` VALUES
  ('001','Tom','Hanks','0000-00-00'),
  ('002','Sandra','Bullock','0000-00-00'),
  ('003','Alan','Rickman','0000-00-00');
CREATE TABLE `stars` (
  `id` int(11) NOT NULL,
  `first_name` varchar(50) DEFAULT NULL,
  `last_name` varchar(50) DEFAULT NULL,
  `dob` date DEFAULT NULL,
  `photo_url` varchar(200) DEFAULT NULL,
  PRIMARY
```
