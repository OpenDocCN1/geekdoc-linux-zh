
QEMU by default sets up some basic NAT networking which is fine for many use cases, but won’t let you, for example, SSH into the VM. Check the box (below left) for more advanced networking options. You can also go ahead and install Elementary OS as if we were doing it for real. When the install finishes select Restart. The virtual optical media will be ejected and you should be able to log in with the credentials you used to install. You should also find that things are a little faster with the live medium, but probably a far cry from a bare metal install.

By default QEMU sets up a basic VGA video card which for some reason could only manage 800x600 on our Elementary install. It should be able to handle much higher resolutions, but there are better options. One is the paravirtualised QXL virtual video device, which offers 2D acceleration and can, when using a suitable viewer, use the SPICE protocol for an even smoother experience. Shut down the VM and try starting it again with the QXL device:

```bash
$ qemu-system-x86_64 -drive file=/mnt/stor/VMs/\.qcow2 -enable-kvm -m 3G -vga qxl
```

Now, inside the guest, if you run `lspci` you should see a line like the following:

```bash
Red Hat, Inc. QXL paravirtual graphic card
```

and you should also have access to higher resolutions via System Settings > Displays. You can also assign more video memory to the QXL device (the default is 16MB, which is enough to handle up to and beyond 1080p at 32-bit depth, but you’ll need more for 4K) by adding an option like `global qxl-vga.vram_size=64MB` to the end of the previous command. There are other settings for manipulating QXL memory – `vgamem` and `ram` – but we’ll leave it to you to figure out the subtleties that separate them. Bear in mind that none of these represent real video memory, and it won’t help with 3D acceleration (don’t worry, we’ll cover this later).

With the default settings our VM emulates an Intel 440FX chipset with a PIIX3 IDE disk controller and a bespoke emulated CPU. This is very simple hardware by today’s standards, and that is a good thing: it makes these things easier to emulate. Besides the QXL video device or the default VGA driver, it’s also possible to mimic an ancient Cirrus Logic GD5446 (this used to be the default in QEMU). However, rather than emulating old devices, a hypervisor can save effort by creating slimline virtual hardware and marshalling data to the appropriate piece of hardware on our actual machine. This technique is known as paravirtualisation, and the magic that enables KVM to use it is known as VirtIO. The QXL device is paravirtualised in the sense that it provides access to software rendering on the host machine, so it’s not going to break any speed records. But a VirtIO hard drive can offer tremendous speed benefits; a VirtIO network adapter can lower latency and accelerate throughput. The VirtIO drivers are included in all Linux distributions, but you’ll need to install drivers for Windows, which you can find at https://fedoraproject.org/groups/virt/virtio-win/direct-downloads/. VirtIO devices can be set up and tuned from the command line, but this rapidly leads to unwieldy commands. It’s much easier to use the Libvirt-powered GUI interface virt-manager, which we conveniently installed earlier.

![](img/7a0a282248f9658f0c87e55744c797b6_72_0.png)

The graphs available from the Performance tab are useful for seeing what your virtual machines are up to.

## VIRTUAL MACHINE MANAGER

In order to use `virt-manager` we need the `libvirt` service to be running, and, since this feature will probably get you hooked on VMs, we may as well set the service to start on each reboot:

```bash
$ sudo systemctl enable --now libvirtd
```

You should now be able to start *Virtual Machine Manager* from your applications menu. Click the *New Virtual Machine* button and a wizard will guide you through the process of building a VM. Choose “Local install media” unless you want to do something else. Once you’ve told `libvirt` about the OS you’re installing you can set up CPUs and memory. Then you’ll need to create a virtual storage volume. By default storage volumes live in `/var/lib/libvirt/images`. If you want them to live somewhere else, then you can add a directory by clicking the green + button from the custom storage dialogue, then create the storage volume there.

Finally there’s an option to choose networking options, the default NAT network is fine, but you may wish to explore vtap devices if you have compiled requirements. Most of these settings can be changed later, but if you need to set up UEFI booting (for example if you’re doing GPU pass through) this needs to be done before the OS is installed, by checking the *Customise configuration* checkbox before clicking *Finish*.

![](img/7a0a282248f9658f0c87e55744c797b6_72_1.png)

That *Customise configuration* checkbox is easy to miss, but we’ll need it later.

## DOUBLE THE VIRTUAL FUN

“QEMU on its own is an emulator, but combined with the power of KVM it becomes a virtualisation tool”

## GPU passthrough

Experience near-native graphics performance in a VM with the magic of PCI passthrough. It’s better than watching rabbits being pulled out of hats!

Lately, Steam Play has been getting a great deal of attention from Linux gamers, and with good reason. It brings a whole raft of titles to the platform, most of which stood zero chance of ever seeing an official port. However, many of the officially blessed titles don’t perform as well on Linux as they do on Windows, and many other titles run into all kinds of bugs, which prevent them being played properly at all. Make no mistake, Valve’s Proton Wine fork and DXVK sponsorship are great, but they’re not going to convince hardcore gamers to switch to Linux anytime soon. Even native Linux ports from the likes of Feral and Aspyr rarely compete performance-wise with their Windows counterparts.

Virtual Function I/O (VFIO) enables the Linux kernel to pass PCI hardware directly to VMs with negligible overhead. This includes complicated hardware such as expensive graphics cards, so you can see where this is going. Besides gaming on a Windows VM, this is useful if you have a deep learning or mining environment set up in a VM. Many people that have this working have reported close to 99 per cent native performance. In order to get this working though, there are several hoops to jump through.

First, so there’s no confusion let’s be clear: This requires two graphics cards, the host OS relinquishes all control of the passed-through GPU to the VM, so it’s as good as dead to it. There are also a bunch of other hardware requirements that we’ve tried to sum up in the box (right). If you’re using two dedicated cards, make sure you have sufficient power to feed them. Theoretically, the one on the host shouldn’t be drawing much power while the VM is busy, but you never know. Modern GPUs have become efficient as well as powerful, but on a busy day the gruntier models can happily draw 250W.

## I need IOMMU

As well as activating it in the BIOS, we need to tell the kernel to use IOMMU by way of some bootloader options, which we can either add to the `linux` line in /boot/grub/grub.cfg, or we can use the recommended drill of adding them to the `GRUB_CMDLINE_LINUX_DEFAULT` line in `/etc/default/grub` and then running `grub-mkconfig`. On an Intel system, the requisite option is `intel_iommu=on`, while on AMD it’s `amd_iommu=on`. Reboot, then run the following script (appropriated from the helpful Arch Wiki VFIO page, which is worth a read. https://wiki.archlinux.org/index.php/PCI_passthrough_via_OVMF):

```bash
#!/bin/bash
shopt -s nullglob
for d in /sys/kernel/iommu_groups/*/devices/*; do
  n=${d#*/iommu_groups/}; n=${n%%/*}
  printf "IOMMU Group %s \"\n" "$n"
  lspci -nns "${d#*/}"
done;
```

PCI hardware can only be passed through in a manner which respects these groupings. If your graphics card (the one you want to pass through) is in the same group as important or complicated looking devices the easiest solution is to move it to another slot and try again. In our case the script produced:

```
***
IOMMU Group 16 01:00.0 VGA ... Hawaii XT [Radeon R9 290X/390X] [1002:67b0]
IOMMU Group 16 01:00.1 Audio device ... Hawaii HDMI Audio [Radeon R9 290/290X / 390/390X] [1002:aa68]
***
```

This is actually a pretty ideal case. The HDMI audio device on our GPU is in its IOMMU group, so we need to pass that through as well, granting our VM both video and audio hardware.

Once kernel drivers bind to our pass-through GPU, neither hell nor high water will persuade them to let go of it, so we need to stop this happening. This is achieved with the `vfio-pci` driver which we need to inform of the pass-through device’s vendor and device IDs (the

![](img/7a0a282248f9658f0c87e55744c797b6_73_0.png)

Yin and yang: we used an Nvidia GTX 680 for the host and a slightly newer, faster Radeon 290 DCX for the guest.

![](img/7a0a282248f9658f0c87e55744c797b6_73_1.png)
