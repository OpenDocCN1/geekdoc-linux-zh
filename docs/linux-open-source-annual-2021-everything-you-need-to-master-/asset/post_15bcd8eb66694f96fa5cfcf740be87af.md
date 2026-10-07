
## QEMU and KVM

Dig deeper and build your own virtual machine at command using the power of Linux.

VirtualBox is all well and good, but there are other people who don't like using Oracle software, and in the past extensions (which enabled graphics acceleration and shared clipboards) weren't free licensed, meaning they couldn't be bundled or installed separately.

This is the longer case and most difficult when the required host and guest modules - mismatched (if guest is running), for example - and the host must be installed manually. These can be installed on all platforms - in running VM by installing Guest Additions from the menu. A virtual CD will be inserted and you'll find a link to install such modules, as well as Windows and MacOS.

Anyway, we were supposed to talk about VirtualBox, not providing advice. So, there's free (but not open source) VMware Player, which allows running a single machine on the desktop and in a user's view which works as much as VirtualBox. However, the virtualization remained not because people could run clunky desktop operating systems within another clunky desktop operating system, because powerful servers could house multiple VMs - saving resources, increasing portability and generally making them work. Workstation Pro is VMware's commercial offering, and there are Hyper-V, Xen and other tools that revolutionized infrastructure management. One of them is cheap QEMU (KVM virtual partitions from there) of Linux Debian and Ubuntu. These are a great way to get what server administration is all about.

When you start doing, you have two choices: KVM and QEMU. KVM is the userspace host and enables the kernel to access the virtualizations of the CPU. QEMU is the userspace utility that thanks to it can emulate virtual hardware for many architectures like Arm, x86/32 and MIPS, and we've already talked about emulation and various architectures so that the actual amount of emulation QEMU has to be reduced to almost zero.

QEMU is a command-line tool, as in our way. Using assistance or building CLIs we won't let you do. Using QEMU is just a matter of:

## VirtIO

We mentioned that virtIO in the QEMU/KVM journey is to emulate hardware, and we're glad to point out that this is a real advantage. So let's talk about such things. It makes sense to tell the version of the OS that it is, and that the hardware it can see or not. In this way we modify the OS (or in this case its drivers) and have the hypervisor present as a paravirtual controller. The framework KVM uses these for its paravirtualization of block devices, video devices, network devices and the increasingly named balloon device (memory management). These drivers need to be installed on the guest, but have been part of the kernel for a long time - so for Linux no guest is required.

```bash
$ qemu-system-x86_64 -qcow2,if -v virtio-net nic,model-virtio -m -enable-kvm
```

if, in the guest you run you will see your VM now has a virtio-powered video. Ethernet and SCSI disk. In order to take advantage of the improved video device you'll need to install a desktop environment where you can do:

```bash
$ sudo apt install ubuntu-gnome
```

![](img/5f8379eaeda572d04307c37d75b0ba5d_71_0.png)

QEMU doesn't look like that, but it's incredibly powerful and enables you to perform destructive actions with no risk of Linux Scratch, how can't he be?, but we'll be a little behind it and try a daily Ubuntu 20.04 image. You can grab it from scratch at http://ubuntu.com/ubuntu-daily-live/current

Now we can commence installation, adjusting paths for the install medium and qcow2 if they are not in the current directory:
`qemu-system-x86_64 -cdrom=ubuntu-server-amd64.iso -boot order=d -drive file=qcow2.img`

By default QEMU allocates 128MB of memory for its machines, which turns out it is near enough to boot, but we need 2GB for this. A window would open, which allows you to click to navigate to the setup guests. By default QEMU provides DHCP and servers to leave the VM with an IP address of the form 10.0.2.number, which you then use with Guest address. Ubuntu can automatically set up SSH for you, which is a Good Thing but we need host-guest networking with QEMU. It also offers you a list of snaps, feel free to install anything you might need. You may want to backup your local image file if you have the VM running to do anything.

While the install is running, or QEMU window is open, you can press Ctrl+Alt+2 to show the QEMU monitor, which allows you to assess the state of QEMU. You will then probably type info to see which KVM is being used. If it says machine is not virtualizing, Oops. That was some way explaining the software, and it only takes a moment to switch to KVM by pressing Ctrl+Alt+1 to go to the VM. Once the install has completed, shut the VM. If you want to reboot, or go back to the machine, then Ctrl+Alt+Del to escape the mouse from the VM's window and it's finished.

Now start the machine with the correct invocation:
`qemu-system-x86_64 -drive file=qcow2,format=qcow2 -m 2G` login with the credentials you invented. Ubuntu will then find its IPv4 and IPv6 addresses, but if you try SSH from the host, you'll find it work. QEMU's default network setup gives the guest:

| Guest | Wind |
| :--- | :--- |
| Desktop | |
| Dashboard | |
| Settings | |
| Language & region | |
| Accounts | |
| Users | |
| Privacy | |
| Network | |
| Sound | |
| Applications | |

If you are running into difficulties, its easy to delete everything and start again from Network settings.

![](img/5f8379eaeda572d04307c37d75b0ba5d_72_0.png)

Once Ubuntu drivers were installed, we need our Ubuntu Server 20.04 VM to access the host (at 10.0.2.2), but not vice versa. Communication between guests is also possible in this configuration. We could set up a device (a network interface) or host-networking, which is what we are going to talk about later. Refer to the Arch Wiki page on QEMU, See: https://wiki.archlinux.org/title/QEMU

If you want more than one VM to use your QEMU bridge:

## DON'T FEAR THE EMULATOR

QEMU is an emulator, but we'll see the amount of emulating it has to be reduced to absolute zero. Helper to (for virt connection). This involves creating a file /etc/qemu/bridge.conf consisting of a single line:
`allow bridge0`

Now we create the bridge, add our Ethernet connection (enp3s0) to connect it to the outside world. If your distro uses NetworkManager (it probably does) then it's better to use nmcli rather than lower-level commands:
```bash
sudo nm connection add type bridge ifname bridge0 master bridge0
sudo nm connection add type bridge-slave ifname enp3s0 master bridge0
```
sudo start QEMU:
`qemu-system-x86_64 -drive file=qcow2,format=qcow2 -m 2G -net tap bridge0`

This VM will use the same network as the host and get an IP from your home router. This thing can be achieved in VirtualBox by visiting the network settings, and changing the type from NAT to Bridge Adapter.

## Into the libvirt

Putting all the pieces together, how show you to make virtualization faster, easier and safer. You might have that from QEMU inc can get quite unnoticed unless you start avoiding them – so it's a script, or use some kind of find for. With Red Hat's libvirt, you'll meet Virtual Machine Manager soon, which is rather an API that provides access to virtualization with libvirt. Libvirt provides a number of hypervisors, virtual disks (or pools), networking (no handcrafting network bridges) and naturally can create and start VMs. VMs might also abstract the users out of the business of running with libvirt, and this is generally good.

This might seem to lead to another layer of complication on something's complicated. That is a reasonable point: if you just want to set up a VM to try something out, it's easy to do with VirtualBox or any other friendly friend. When libvirt comes into your management, it can take care of storage (size). Since we are running a VM in our development environment and starting, crashing us to log out. With that VM we'd find in a safe state, the same process running it with QEMU or KVM would be much like

With Libvirt – known slightly confusingly as domain – run by a separate user, or if a local VM in the background that they're playing with a VM needs to be connected to. In that way it works like connecting to a network machine. In fact another libvirt is able to run multiple machines with simple boxes without being between the scenes to totally abstract the difference, so the interface you can connect to a machine, virtual machine, or a remote.

## KEEPING OUR VM SAFE

The CPU vulnerability that was opened in January 2018 with Spectre and Meltdown shows no of ceasing to stop. Vulnerabilities emerge, with special attention to virtualization. L1TF and LDR are public. This is another attack – albeit by pretty means – access memory that they shouldn't be. One of the major concerns is that on a host running multiple VMs, allowing one VM to read the other's memory. We use AMD's secure enclave (SEV).

## Installing libvirt

We can install all the required bits in Ubuntu from Virtual Machine Manager (aka virt-manager) from the Cloud giants host VMs on shared memory, so they can access data, so this is a grave concern. And VMs hosts themselves need to have fixes applied and rebooted to be safe, and if you ask a VPS provider out of yours they should be in touch with you too. If they haven't, you might not consider the change. In the meantime, if your libvirt is at https://mockvirt.com/ it will be vulnerable:

```bash
sudo apt install libvirt-manager
```

If you skipped the pages (previous above), or if you need to add libvirt to your group, you'll need to log out and back in before the services work.

Keeping track of so CPU vulnerabilities is a full occupation.
