
## Installing Kali Linux

From the home page, click the **Downloads** link at the top of the page, and it will take you to the Downloads page. Here, you’ll be faced with multiple download choices, something like the figure below.

These are the different versions of Kali for various systems.

It’s important to choose the right download. Along the left side of the table, you will see the *image name*, which is the name of the version that the link downloads. For instance, the first is Kali Linux 64-Bit, meaning it’s the full Kali Linux, and is suitable for 64-bit systems—most modern systems use a 64-bit Intel or AMD CPU. To determine what type of CPU is on your system, go to Control Panel > System and Security System, and it should be listed. If you’re a 64-bit system, download and install the 64-bit version of the full Kali (not Light or Lxde, or any of the alternatives).

If you are running an older computer with a 32-bit CPU, you will need to install the 32-bit version that appears lower on the page.

You have a choice of downloading via HTTP or Torrent. If you choose HTTP, Kali will download directly to your system and place the image in your Downloads folder. The TORRENT download is the peer-to-peer download used by many file-sharing sites. You will need a torrenting application like BitTorrent to use this. The Kali file then will be downloaded to the folder in which the torrenting application stores its downloads.

There are other versions for other types of CPUs, such as the commonly used ARM architecture found in so many mobile devices. If you are using a Raspberry Pi, a tablet, or other mobile device (phone users will likely prefer Kali NetHunter), make certain you download and install the ARM architecture version of Kali by scrolling down to Download ARM images and clicking **Kali Arm Images**.

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_101_0.png)

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_101_1.png)

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_101_2.png)

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_102_0.png)

## Setting Up Virtualization

Now that you have Kali downloaded, but before you install anything, I want to talk a bit about virtual machines. As I mentioned above, Virtual Machine (VM) technology allows you to run multiple operating systems from one piece of hardware like your laptop or desktop. This means that you can continue to run your familiar Windows, Mac or Linux operating system and run a virtual machine of Kali Linux inside that operating system. You don't need to overwrite your existing OS to learn hacking.

Let's install VirtualBox as our virtualization system.

### Installing VirtualBox

You can download VirtualBox at www.virtualbox.org. You should see a Downloads button in the left menu. Click the Downloads button, which will take you to the screen shown below. Select the download link for your computer's current operating system, which will host VirtualBox VM. Make sure to download the latest version of VirtualBox.

When the download has completed, click the setup file and you will be greeted by a familiar Setup Wizard like below.

Click **Next**, and you should be greeted with the Custom Setup screen.

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_103_0.png)

#### Welcome to VirtualBox!

The left part of this window lists all virtual machines and virtual machine groups on your computer. The list is empty now because you haven't created any virtual machines yet.

In order to create a new virtual machine, press the **New** button in the main tool bar located at the top of the window.

You can press the **F1** key to get instant help, or visit [www.virtualbox.org](www.virtualbox.org) for more information and latest news.

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_104_0.png)

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_105_0.png)

From this screen, simply click **Next**.

Keep clicking **Next** until you get to the Network Interfaces warning screen, and then just click **Yes**.

Click **Install** to begin the process. During this process, you will likely be prompted several times about installing *device software*. These are the virtual networking devices necessary for your virtual machines to communicate. Click **Install** for each one.

When the installation is complete, click **Finish**.

### Setting Up Your Virtual Machine

Now let’s get you started installing our virtual machines. VirtualBox should open once it has installed—if not, open it—and you should be greeted by the VirtualBox Manager, as seen below.

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_106_0.png)

Since we will be creating a new virtual machine with our Kali Linux, click **New** in the upper-left corner.

This opens the **Create Virtual Machine** window as seen below.

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_107_0.png)

Give your machine a name in the first window (any name is okay, but I simply used Kali) and then select **Linux** from the Type pull-down menu. Finally, select **Debian (64-bit)** from the third pull-down (unless you are using the 32-bit version of Kali, in which case select the Debian 32-bit version). Click **Next**, and you’ll see a screen like below. Here, we need to select how much RAM we want to allocate to this new virtual machine.

As a rule of thumb, I don’t recommend using more than 25% of your total system RAM. That means if you have installed 4GB on your physical or host system, then select just 1GB for your virtual machine, and if you have 16GB on your physical system, then select 4GB. The more RAM you give your virtual machine, the better and faster it will run, but you must also leave enough RAM for your host operating system and our other virtual machines you might want to run simultaneously. Your virtual machines will not use any RAM when you are not using them, but they will use hard drive space.

Click **Next**, and you’ll get to the Hard disk screen. Choose **Create a virtual hard disk now** and click **Create**.

In the next screen, you can decide whether you want the hard drive you are creating to be allocated dynamically or at a fixed size. If you choose **Dynamic allocated**, the system will *not* take the entire maximum size you allocate for the virtual hard disk until you need it, saving more unused hard drive space for your host system. I suggest you select Dynamically allocated.

Click **Next**, and you’ll choose the amount of hard drive space to allocate to the VM and the location of the VM.

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_108_0.png)

#### Create Virtual Hard Disk

**File location and size**

Please type the name of the new virtual hard disk file into the box below or click on the folder icon to select a different folder to create the file in.

Kali

Select the size of the virtual hard disk in megabytes. This size is the limit on the amount of file data that a virtual machine will be able to store on the hard disk.

4.00 MB | 25.2 GB | 2.00 TB

[Create] [Cancel]

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_110_0.png)

The default is 8GB. I usually find that to be a bit small and recommend that you allocate 20–25GB as a minimum. Remember, if you chose to dynamically allocate hard drive space, it won’t use the space until you need it, and expanding your hard drive after it has already been allocated can be tricky, so better to err on the high side.

Click **Create**, and you’re ready to go!

## Installing Kali in the VM

At this point, you should see a screen like that below. Now you’ll need to install Kali. Note that on the left of the VirtualBox Manager, you should see an indication that Kali VM is powered off.

Click the Start button (green arrow icon).

The VirtualBox Manager will then ask where to find the startup disk. You've already downloaded a disk image with the extension `.iso`, which should be in your *Downloads* folder (if you used a torrent to download Kali, the `.iso` file will be in the *Downloads* folder of your torrenting application). Click the folder icon to the right and navigate to the *Downloads* folder, and select the Kali image file.

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_111_0.png)
