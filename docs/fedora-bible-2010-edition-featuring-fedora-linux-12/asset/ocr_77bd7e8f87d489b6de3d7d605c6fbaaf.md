More than a dozen selections in the left column of this screen let you see details about your guests. Here are descriptions of some of those selections and where you have opportunities to configure your guests:

+   - **Performance** — Watch your CPU, memory, disk, and network usage live.
+   - **Processor** — See the number of allocated CPUs and possibly change that allocation.
+   - **Memory** — View how much memory is allocated to the guest and possibly change that.
+   - **Boot Options** — Choose if the guest autostarts and where the guest boots from.
+   - **Disk hda and hdc** — See details of your virtual hard disk (hda) and CD drive (hdc).
+   - **NIC** — View (and possibly change) your network interface card’s MAC address.
+   - **Mouse** — See your mouse configuration.
+   - **Display vnc** — See the VNC server address and port for viewing the guest.
+   - **Sound, Serial, Video** — See driver information for the virtual sound card, serial ports, and video card.

To use your virtual guest, you can simply click inside the Virtual Machine window for that guest once it is open and begin using it as you would any operating system from the system console. Because you are using the guest from a window, and not from the entire screen as you would normally, there are a few special features you should be aware of as you move around:

+   - **Grabbing the mouse pointer** — When you use a virtual guest, or any VNC client, clicking inside its window causes your mouse pointer to be trapped within that window. Press Ctrl+Alt to release the pointer back to your entire desktop.
+   
+   - **Using function keys** — If you need to do things such as view virtual windows within the console session to your guest, the functions keys won’t work as expected. In other words, pressing Ctrl+Alt+F2 will show the second virtual terminal of your host system, not your guest system.

To pass those and other key sequences to your guest system, select Send Key from the virtual machine window and choose the key sequence you want. For example, you could select Ctrl+Alt+F1 (to see the first virtual console on your guest), Ctrl+Alt+Backspace (to kill your guest desktop session), Ctrl+Alt+Delete (to reboot the guest), or printscreen (to take a screenshot of the screen, the same effect as pressing the Print Scrn button).

+   - **Getting to the boot prompt** — If you are using Xen instead of KVM, when you go through VNC to view your guest, the view bypasses the boot loader when the system comes up. If you can’t boot your guest properly, there’s a way to get to the boot loader screen and change boot options. To do that, select Shutdown to turn off your guest. Then, from the command line, type the following line (replacing myguest with your guest system’s name):

```
# xm create -c myguest
```