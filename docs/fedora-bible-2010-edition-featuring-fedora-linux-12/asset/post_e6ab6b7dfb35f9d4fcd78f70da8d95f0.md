
## Viewing guest host details
- **View guest host details** — To see details about a guest system, click on the host in the Virtual Machine Manager window and select Edit → Host Details. From the Host details window, you can watch CPU and memory usage from the Overview tab. Select Virtual Networks to see details about your network device and IP addresses. The Storage tab lets you see the storage areas available to your guest.
- **Pause the guest** — Right-click on a guest entry and select Pause. All processing pauses on the guest until you select Pause again to resume.
- **Delete the guest** — You can permanently remove a virtual guest you no longer need. Make sure the guest is shut down. Then select Edit → Delete. You are then given the choice of deleting the guest, as well as its associated storage volume.

The actions just described can also be done as you display a text-based or graphical console of the guest. Opening and using the guest from your Fedora desktop is described in the next section.

## Viewing and using guests

To open a guest, double-click on the guest’s entry in the Virtual Machine Manager window. The window that appears displays a graphical or text-based console to use the guest. One of the first things you might want to do is view and change details about your guest.

Click the “i” information icon in the toolbar to see details about how the guest is configured. Figure 25-5 shows an overview of the virtual guest (its name, run status, architecture, and so on).

![](img/c78bdcb5b7842a0d73dcc98921f872a2_934_0.png)

**Figure 25-5**: View and modify information about your virtual guest.

More than a dozen selections in the left column of this screen let you see details about your guests. Here are descriptions of some of those selections and where you have opportunities to configure your guests:

- **Performance** — Watch your CPU, memory, disk, and network usage live.
- **Processor** — See the number of allocated CPUs and possibly change that allocation.
- **Memory** — View how much memory is allocated to the guest and possibly change that.
- **Boot Options** — Choose if the guest autostarts and where the guest boots from.
- **Disk hda and hdc** — See details of your virtual hard disk (hda) and CD drive (hdc).
- **NIC** — View (and possibly change) your network interface card’s MAC address.
- **Mouse** — See your mouse configuration.
- **Display vnc** — See the VNC server address and port for viewing the guest.
- **Sound, Serial, Video** — See driver information for the virtual sound card, serial ports, and video card.

To use your virtual guest, you can simply click inside the Virtual Machine window for that guest once it is open and begin using it as you would any operating system from the system console. Because you are using the guest from a window, and not from the entire screen as you would normally, there are a few special features you should be aware of as you move around:

- **Grabbing the mouse pointer** — When you use a virtual guest, or any VNC client, clicking inside its window causes your mouse pointer to be trapped within that window. Press Ctrl+Alt to release the pointer back to your entire desktop.
- **Using function keys** — If you need to do things such as view virtual windows within the console session to your guest, the function keys won’t work as expected. In other words, pressing Ctrl+Alt+F2 will show the second virtual terminal of your host system, not your guest system.

To pass those and other key sequences to your guest system, select Send Key from the virtual machine window and choose the key sequence you want. For example, you could select Ctrl+Alt+F1 (to see the first virtual console on your guest), Ctrl+Alt+Backspace (to kill your guest desktop session), Ctrl+Alt+Delete (to reboot the guest), or printscreen (to take a screenshot of the screen, the same effect as pressing the Print Scrn button).

- **Getting to the boot prompt** — If you are using Xen instead of KVM, when you go through VNC to view your guest, the view bypasses the boot loader when the system comes up. If you can’t boot your guest properly, there’s a way to get to the boot loader screen and change boot options. To do that, select Shutdown to turn off your guest. Then, from the command line, type the following line (replacing myguest with your guest system’s name):

```
# xm create -c myguest
```

A text-based version of the bootloader should appear. You will probably have to press a key to prevent the system from booting the default boot entry. Edit the boot loader as needed (for example, you may want to add a `1` to the end of the kernel line to enter run level 1) and have the bootloader continue. After that, press `Ctrl+Alt` to close the console window and return to your regular `VNC` view of the guest.

Besides the issues just mentioned, you can use your virtual guest from within the VNC window as you would any operating system directly from the desktop. When you are done using it for the moment, just close the window. While this closes your view to the running system, it does not stop that system from running. Just double-click the guest's entry in the Virtual Machine Manager window and you can begin viewing it again.

## Cloning guests

Once you have a virtual guest working the way you want it, why not repeat your fun? By cloning your virtual guest you can have a copy of that guest that can run on your host system or to run on another system. Here's how you clone a virtual guest:

1. **Pause or shut down the guest.** If the guest you want to clone is running, select Shut Down from the running guest. Then choose Shut Down or Force Off. If you prefer, you can simply pause the guest by selecting the Pause button.
2. **Select Clone.** From the guest's Virtual Machine window, select `Virtual Machine → Clone`. A Clone Virtual Machine window appears, as shown in Figure 25-6.

![](img/c78bdcb5b7842a0d73dcc98921f872a2_936_0.png)

**Figure 25-6:** Create clones of useful virtual guests.

3. **Identify the clone.** Select or type in the following information:
    - **Name** — The current guest name with a “-clone” added is assigned to the clone by default. You can change that to any name you like.
    - **Networking** — If you are using bridging (the default) on the guest, the same type of networking is assigned to the clone. (Click Details to see more about the device.)
    - **Storage (disk image)** — A storage area of the same size and type used by the guest is created in the same directory (such as `/var/lib/libvirt/images`). The text “-clone” is included in the image name just before the `.img` suffix. (Click Details in the storage box if you want to change the name or location of the image.)
    - **Storage (removable media)** — If your machine has removable media, such as a CD drive, that will appear under the Storage heading and identify it as being shareable from the clone.
4. **Start the cloning.** Select the Clone Virtual Machine button. A new storage area is created, along with the new virtual guest itself.

The cloned virtual guest should appear in the Virtual Machine manager window. You can run it from there alongside your other virtual guests. If you want to move the clone to another system or back it up, it is located under the `/etc/libvirt` directory structure. The storage area is under `/var/lib/libvirt/images`, unless you saved it to a different location.

With different guest names and clone names, the guests can both run on the same system without conflict. When they boot, they will use their own resources and, by default, have network interfaces with different IP addresses.

# Using Command-Line Tools to Manage Virtual Guests

Even with nice graphical interfaces available with KVM virtualization, many Linux experts prefer to work from the command line to build and manage virtualization. The following sections list tools for creating virtual guests, building storage volumes, and managing your guest systems.

## Creating and converting storage volumes

The `qemu-img` is a versatile tool for creating storage volumes, checking volumes, and converting them to different formats. To use the `qemu-img` command, you must have the qemu-img package installed.

### Getting information about a storage volume

If you have some existing storage volumes (created by virt-manager or some other tools), you can get information about a volume using `qemu-img` with the `info` option. For example:

```
# qemu-img info Fedora12.img
```
