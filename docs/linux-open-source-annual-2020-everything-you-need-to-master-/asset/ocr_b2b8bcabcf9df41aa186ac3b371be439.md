# ## VirtualBox

Enjoy a gentle introduction to the world of virtual boxes with the aptly named VirtualBox.

![](bbox=[0.68, 0.05, 0.93, 0.19])

**M**aking your first virtual machine is easy – the hardest part is deciding which platform to use. VMware and VirtualBox provide free tools for all operating systems (including Linux). On Windows you can use Hyper-V which, with its new Quick Create feature, can spin up an Ubuntu instance faster than you can say “Microsoft’s patent practice evolving in lock-step with the company’s views on Linux and open source more generally.” We’re going to go with **VirtualBox** because it’s licensed under the GPL version 2 (except for

![](bbox=[0.06, 0.35, 0.53, 0.58])

> The shared clipboard option enables the luxury of copying and pasting between guest and host. Small caveat: this doesn’t share the X11 mid-click clipboard, just the desktop one.

the Extension Pack which provides features like USB passthrough and NVMe devices, not to be confused with the Guest Additions which are now GPL too) and because it looks the same on all OSes. Follow the step-by-step guide (below) to getting started, or if you already know the ropes then read on and delve into some of its lesser-known features.

# ### Virtual tweaks

Let’s assume you’ve followed our guide, booted the install medium and installed Ubuntu into your **VirtualBox**. If not, perhaps you should – just as in the real world, live OSes are much slower than installed ones in the virtual world. When the VM starts up I see a message about mouse pointer integration. This is a terrifyingly helpful feature that enables seamless mouse movement between guest and host. When you use guest OSes that don’t support this feature, it’s necessary to use a keyboard shortcut (right-Ctrl) to free the pointer from its imprisonment within the guest window.

The default **VirtualBox** settings work fine for installing most Linux guest OSes, but there’s always room for improvement. The first thing you probably noticed is that the VM has a low resolution and that moving/resizing windows is painfully slow. This is because our virtual video card has a paltry 16MB of memory and no acceleration features. We’ll need to shut down the VM to address this. Once that’s done, select the VM from the list on the left and hit the Settings button in the toolbar and proceed to the Display section. Here you can define

# ### INSTALL AND CONFIGURE VIRTUALBOX

+   1. **Download virtualbox**
If you’re on macOS or Windows, head over to **www.virtualbox.org** and follow the download links. Then run the downloaded binary to install it. If you’re on Linux, **VirtualBox** is almost certainly in your distro’s repos. On Ubuntu, installing it is just a matter of **sudo apt install virtualbox.** Fire it up from the Applications menu (or however your OS calls it).

+   2. **Create a new VM**
Hit the **New** button in the top-left of the **VirtualBox** interface. We’ll make an Ubuntu 18.10 VM, which we’ve called **LXF-Ubuntu-VM** here but you can call it whatever you want. Set the **Machine Type** box to **Linux**, and the **Version** box to **Ubuntu (64-bit)**, unless you want a 32-bit VM. If you’re feeling confident, click the **Expert Mode** button, otherwise hit **Next.**

+   3. **Choose your memory size**
How much memory you allocate to your virtual machine depends on how you want to use it and how much RAM the host machine has. Modern desktops and applications (particularly web browsers) will happily chomp through 2GB, where as booting to the console requires very little. If you allocate too much memory to your VM, the host will suffer.