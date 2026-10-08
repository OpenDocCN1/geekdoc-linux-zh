# QEMU and Libvirt

Learn some more advanced ways and means of manipulating your VMs...

**V** *irtualBox* is a great choice for getting started with virtualisation. It has a catchy name, a friendly interface and it’s cross-platform, but there are other options on Linux, too.

Many people actively avoid *VirtualBox* because of its association with Oracle (seen by some as a litigious corporate behemoth) which inherited the software from Sun, which it acquired in 2010. QEMU is a tool that’s much more aligned with standard Linux practices (y’know, interminable command line options, abstruse configuration files and unforgiving error messages). QEMU on its own is an emulator, but combined with the power of KVM it becomes a high-fidelity virtualisation tool.

Elsewhere, *Libvirt* provides a platform for easy management of QEMU (and other) VMs. It takes the headache out of defining virtual networks and storage, and allows VMs to be managed and accessed remotely. For a more thorough explanation of these three layers, see virtualisation guru *Berto Garcia’s comments in LXF234*. *Libvirt* can in turn be managed by the excellent *virt-manager*, which gives access to most QEMU options

# » INTRODUCING VIRGL

The Virtual Machine Manager GUI enables us to choose the QXL video device with the click of a button. However, it also enables us to go one deeper and match (and perhaps even surpass) *VirtualBox’s* 3D acceleration capabilities.

In our interview with Colaboba’s graphics guru *Daniel Stone* (see LXF243), he mentioned the *VirGL* (pronounced *Virgil*) project, and its use in Chrome OS’s *Crosvm* hypervisor. *VirGL* can pass OpenGL calls directly to the host’s GPU, allowing 3D acceleration within the guest. Activating *VirGL* from *virt-manager* (see over the page) is surprisingly easy: from the Video section just select *Virtio* as the model and tick the 3D acceleration box. Then in the Display Space section change the Listen type to *None* (*VirGL* doesn’t work over TCP), and check the *OpenGL* box. You may also need to manually select your video device from the box that appears below, even if you only have one. Within the VM you can check that *VirGL* is active by running

```
`$ dmesg | grep drm`
and look for
```

```
`[drm] virgl 3d acceleration enabled`
```

![](bbox=[0.55, 0.2, 0.95, 0.37])

via a clean and friendly graphical interface. But let’s do things the old way first. To install *QEMU* (as well as the required *Libvirt* bits we’ll use later) on Ubuntu 18.04 (and derivatives) do the following:

```
`$ sudo apt install sudo apt install qemu-kvm libvirt-client libvirt-daemon-system bridge-utils virt-manager`
```

# My first QEMU VM

Before we can have a virtual machine, we need some virtual storage. The simplest way to do this is to use *qemu-img*, as follows:

```
`$ qemu-img create -f qcow2 lxf.qcow2 2.0G`
```

This will create a dynamic QCOW2 image, so in this case it won’t immediately swallow up 20GB of disk space. Do make sure you create it in a location where you can safely grow to that size though, because if your root partition runs out of space then terrible things can happen. It’s possible to use statically sized raw images too. These may offer performance benefits in some situations and won’t incur storage overhangs as you add data to them, but we less robust when your VM crashes.

We define the specifics of our VM by way of command line options. As you can imagine, there are probably enough of them to fill an issue of *Linux Format*, so we’ll concentrate on the essentials first. We’ll use an Elementary OS ISO (which you can find on our DVD, but you’ll want to copy it to a faster drive) in this example, but feel free to boot the OS of your choice. You can equally well specify */dev/cdrom* instead of an ISO file if you want to use actual media. Here’s how to fire up our VM and allocate it 3GB of memory (a reasonable amount for desktop Linux):

```
`$ qemu-system-x86_64 -cdrom elementaryos-5.0-stable 20181016.iso -drive file=lxf.qcow2 -enable-kvm -m 3G`
```

Note the *-enable-kvm* option here: QEMU on its own is just an emulator, so we don’t let it use KVM then everything is emulated and so things will go slowly. Very slowly. If we explore the live environment (using the Try Elementary option) you should find that browsing the internet works, but pinging hosts doesn’t.

You’ll never have to see this warning again when running Mint in a VM

If you need yet more graphics performance then check out our guide to GPU passthrough over the page.

![](bbox=[0.05, 0.78, 0.3, 0.93])