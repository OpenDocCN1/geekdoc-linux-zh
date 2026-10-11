
$ sudo apt-get install cpu-checker
$ sudo kvm-ok

The output of the above command indicates whether or not the CPU supports the proper CPU extensions that are needed by KVM.

Note that there is actually a more manual way you are able to check for virtualisation support. You can check the flags set for the CPU in the `/proc/cpuinfo` file. Using the popular command `grep`, you can search that file for Intel-VT support (vmx) or AMD-V support (svm). This can be done in the following way:

$ grep -E'(svm|vmx)' /proc/cpuinfo

In the output of the above command, you should see either the vmx or svm flag and not both. If you do not get any output from the grep command, it means that your computer’s CPU does not support KVM virtualisation.

Next, you need to enable virtualisation support in the BIOS. If you think that your computer can support virtualisation, but the appropriate flag is not set, then you may need to turn on virtualisation support in the BIOS. In order to do this, first reboot your computer and interrupt the boot process when you see the first BIOS screen. In the BIOS screen that you see, look for something like a CPU or Performance heading (it varies depending on manufacturer) and select it. Then you need to look for a virtualisation selection such as ‘Intel Virtualisation Tech’ and enable it. Once you’ve changed the virtualisation BIOS settings, save and ensure that you power down the computer so that the BIOS settings will come into effect.

If possible, try to use a 64-bit computer as your virtualisation host. Some operating systems do not support KVM on 32-bit systems. One drawback of a 32-bit KVM host is that each VM is limited to 2GB of memory. In order to check whether your computer is a 32-bit or 64-bit, you can check the CPU flags.

$ sudo egrep lm /proc/cpuinfo

![](img/628186dda7facdc011bf39c938de3975_44_0.png)

The flag `lm` stands for long mode. If this flag is present, then you can be sure that the processor is a 64-bit processor.

Check the available RAM and disk space. Since you will be running multiple operating systems on one physical computer, the amount of RAM and disk space needed is likely to need to be multiplied. Ensure that you have enough memory to service the host and all the VMs you plan to run at the same time. You can check your available memory by using a `free` command:

$ free -m

![](img/628186dda7facdc011bf39c938de3975_44_1.png)

As you evaluate how much memory is needed, you can use a command such as `top` to get a sense of how much memory you require.

For disk space, you want to make sure that there is plenty available in the directory that will store the disk images used by the VMs. By default, the location is `/var/lib/libvirt/images`. You can try the `df` command to check the disk space available at that location.

Note that the `/var/lib/libvirt/images` directory will not be created until the `libvirt-bin` package is installed. So, use the `/var/lib` directory if it is not installed yet, as shown in the following line:

$ df -h /var/lib

## Virtual Machines in a nutshell

A virtual machine can be considered as a computer program that creates a virtual computer system. This virtual computer machine runs as a process in a window on your current operating system. You can boot an operating system installer disc (or live CD) inside the virtual machine, and the operating system will be tricked into thinking it’s running on a real computer. It will install and run just as it would on a real, physical machine. Whenever you want to use the operating system, you can open the virtual machine program and use it in a window on your current desktop. It is important to note here that virtual machines add some overhead, so they won’t be as fast as if you had installed the operating system on real hardware.

> “A virtual machine can be running Windows, Fedora, another Linux system or just about any other operating system you want”

### Tutorial Virtualisation

There are three software components that you need to add so that you can perform KVM virtualisation. They are:

- **libvirt** – This provides an interface for the virtualisation software
- **qemu** – This emulates PC hardware for the virtual machines
- **bridge-utils** – This offers a way to bridge your networking from the virtual machines through the host

You can then run the following **apt-get** commands so that the basic software that is needed for KVM virtualisation will be installed:

`$ sudo apt-get install libvirt-bin kvm bridge-utils qemu-common qemu-kvm qemu-tui`

In addition to the basic software needed for KVM virtualisation, you can also add a graphical interface for managing virtual machines. Use the following command to install the **virt-manager** graphical software for managing the virtual machines:

`$ sudo apt-get install virt-manager`

When we have the virt-manager installed, we have the choice of managing our virtual machines from a graphical interface or from the command line. In the next step, we need to ensure that the user account that we want to use to manage virtualisation is configured to do so.

![](img/628186dda7facdc011bf39c938de3975_45_0.png)

If the user account you are going to use to manage KVM is not a member of the libvirtd group, then that user needs to be added to the group. Say for example, if you want the user account **james** to manage virtualisation, then you will be able to add this user to the libvirtd group as shown below:

`$ sudo adduser james libvirtd`

You may need to reboot your system to make sure that all the necessary services are up and running and that the user account that you have added to the libvirt group is logged in and ready.

The Virtual Machine Manager (**virt-manager**) graphical interface is a very popular tool for managing your KVM virtual machines. Before using any of the commands such as **virt-install** (to install a new virtual machine) or **virt** (virtual machines), it’s a good idea to try out virt-manager. It can lead you through the creation of your first virtual machine in an intuitive way. A few things that you need to focus on before starting with virt-manager are ISO images – you need to download the ISO images of the operating system you either want to install or run live as a virtual machine, and starting **virt-manager** – you can run **virt-manager** from the command line as the user you added to the KVM group. You should be able to see the Virtual Machine Manager window.

Another useful way to manage your virtual machines is through the commands. There are various reasons why you may need to go for commands to manage the virtual machines – the most significant reason being you may want to run commands to work with the virtual machines from a shell script. To get started, you can use the **virt-manager** command to install a virtual machine. With **virt-clone**, you can clone an existing virtual image. For managing virtual machines, you can use the **virsh** command. The virsh command will list the information about the virtual machines as well as help in the starting, stopping and rebooting of virtual machines.

All you need to do to create a virtual machine is to pass the required options to the **virt-install** command. Note that before you use **virt-install**, you need to create a storage image and this can be done by using the **qemu-img** command. With the **qemu-img** command, you can create image files that the virtual machines can utilise as their storage media. Note that for the installer, the images look like regular hard disks. Let us take a quick look at the supported image formats.

- **Raw** – This is the default image type for **qemu-img**. It is the simplest image type and typically used when we need to export the image to the other virtual environments

### Virtual Machine Programs

There are various virtual machine programs for you to choose from. The most popular ones are VirtualBox and VMware Player. **VirtualBox** is widely used as it is open source and completely free. You can also use **VMware Player** on Linux as a free and basic virtual machines tool. The best practice is to start with a **VirtualBox** and if it does not work properly, you can try VMware Player.
