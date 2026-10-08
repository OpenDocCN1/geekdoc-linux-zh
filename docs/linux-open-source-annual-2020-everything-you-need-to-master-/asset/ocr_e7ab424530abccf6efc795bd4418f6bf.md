QEMU by default sets up some basic NAT networking which is fine for many use cases, but won’t let you, for example, SSH into the VM. Check the box (below left) for more advanced networking options. You can also go ahead and install Elementary OS as if we were doing it for real. When the install finishes select Restart. The virtual optical media will be ejected and you should be able to log in with the credentials you used to install. You should also find that things are a little faster with the live medium, but probably a far cry from a bare metal install.

By default QEMU sets up a basic VGA video card which for some reason could only manage 800x600 on our Elementary install. It should be able to handle much higher resolutions, but there are better options. One is the paravirtualised QXL virtual video device, which offers 2D acceleration and can, when using a suitable viewer) use the SPICE protocol for an even smoother experience. Shut down the VM and try starting it again with the QXL device:

```
$ qemu-system-x86_64 -drive file=/mnt/stor/VMs/\n/qcow2 -enable-kvm -m 3G -vga qxl
```

Now, inside the guest, if you run `lspci` you should see a line like the following:

```
**Red Hat, Inc. QXL paravirtual graphic card**
```

and you should also have access to higher resolutions via System Settings>Displays. You can also assign more video memory to the QXL device (the default is 16MB, which is enough to handle up to and beyond 1080p at 32-bit depth, but you’ll need more for 4K) by adding an option like `globol qxl-vga.vram_size=64MB` to the end of the previous command. There are other settings for manipulating QXL memory – `vgamem` and `ram` – but we’ll leave it to you to figure out the subtleties that separate them. Bear in mind that none of these represent real video memory, and it won’t help with 3D acceleration (don’t worry, we’ll cover this later).

With the default settings our VM emulates an Intel 440FX chipset with a PIIX3 IDE disk controller and a bespoke emulated CPU. This is very simple hardware by today’s standards, and that is a good thing: it makes these things easier to emulate. Besides the QXL video device or the default VGA driver, it’s also possible to mimic an ancient Cirrus Logic GD5446 (this used to be the default in QEMU). However, rather than emulating old devices, a hypervisor can save effort by creating slimline virtual hardware and marshalling data to the

![](bbox=[0.05, 0.75, 0.42, 0.92])

The graphs available from the Performance tab are useful for seeing what your virtual machines are up to.

# **VIRTUAL MACHINE MANAGER**

In order to use `virt-manager` we need the `libvirt` service to be running, and, since this feature will probably get you hooked on VMs, we may as well set the service to start on each reboot:

```
$ sudo systemctl enable --now libvirtd
```

You should now be able to start *Virtual Machine Manager* from your applications menu. Click the *New Virtual Machine* button and a wizard will guide you through the process of building a VM. Choose “Local install media” unless you want to do something else. Once you’ve told `libvirt` about the OS you’re installing you can set up CPUs and memory. Then you’ll need to create a virtual storage volume. By default storage volumes live in `/var/lib/libvirt/images`. If you want them to live somewhere else, then you can add a directory by clicking the green + button from the custom storage dialogue, then create the storage volume there.

Finally there’s an option to choose networking options, the default NAT network is fine, but you may wish to explore vtap devices if you have compiles requirements. Most of these settings can be changed later, but if you need to set up UEFI booting (for example if you’re doing GPU pass through) this needs to be done before the OS is installed, by checking the *Customise configuration* checkbox before clicking *Finish*.

![](bbox=[0.45, 0.48, 0.85, 0.58])

That *Customise configuration* checkbox is easy to miss, but we’ll need it later.

appropriate piece of hardware on our actual machine. This technique is known as paravirtualisation, and the magic that enables KVM to use it is known as VirtIO. The QXL device is paravirtualised in the sense that it provides access to software rendering on the host machine, so it’s not going to break any speed records. But a VirtIO hard

# **DOUBLE THE VIRTUAL FUN**

“QEMU on its own is an emulator, but combined with the power of KVM it becomes a virtualisation tool”

drive can offer tremendous speed benefits; a VirtIO network adapter can lower latency and accelerate throughput. The VirtIO drivers are included in all Linux distributions, but you’ll need to install drivers for Windows, which you can find at [https://fedoraproject. org/groups/virt/virtio-win/direct-downloads/](https://fedoraproject. org/groups/virt/virtio-win/direct-downloads/). VirtIO devices can be set up and tuned from the command line, but this rapidly leads to unwieldy commands. It’s much easier to use the Libvirt-powered GUI interface virt-manager. Which we conveniently installed earlier.