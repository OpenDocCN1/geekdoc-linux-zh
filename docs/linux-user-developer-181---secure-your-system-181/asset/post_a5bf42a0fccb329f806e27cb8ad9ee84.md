
## GNOME Boxes
Not quite the box of tricks you might be expecting

![](img/fb76008333fb7aef815b136f9f1afe5f_81_0.png)

For some distributions, Boxes offers the Express Install option to preconfigure the VM, for example by creating a user.

### Usability
This virtualiser has a very approachable interface. To create a new virtual machine, you can either enter the URL from which the application will fetch an image and boot off it or point it to a locally available ISO. The application, however, offers extremely limited customisability options so you can only adjust the amount of RAM and maximum disk size it can occupy.

### Advanced features
If Boxes finds other libvirt-managed VMs on the computer, you’ll get an option to import them. It can also clone VMs and enables you to take snapshots with a single click that you can then rename and revert to with ease. Also, you can point Boxes to a remote VNC server or oVirt and libvirt brokers.

### Native hardware support
Embedded in the VM’s Preferences menu is the option to connect to devices on the host, including the webcam and any attached USB devices. When toggled, the device shows up in the output of the dmesg command on the guest, like they should. However, only the USB drives connected to the host worked as advertised and appeared inside the VM without issues.

### Integration with the host
Once the VM is up and running, Boxes behaves pretty decently. The sound works inside the VMs without any issues and you can also copy and paste text between the host and VM. However, there’s no such option for conducting file transfers.

### Overall
Boxes is a very user-friendly option that supports all the essential features to help a virtualisation débutante experience the essential features of virtualisation without any of its hassles.

![](img/fb76008333fb7aef815b136f9f1afe5f_81_1.png)

## QEMU
The Vulcan’s virtualiser, which is a crude solution but effective.

![](img/fb76008333fb7aef815b136f9f1afe5f_81_2.png)

While it’s well documented, grappling with CLI utilities to create and control virtual machines isn’t everyone’s cup of tea.

### Usability
QEMU has a rich set of features, but these come at the cost of usability. The application is essentially a command-line utility and a typical install dumps a huge subset of qemu-prefixed tools for emulating different architectures. Front-ends like Qemu Launcher and AQEMU do a good job of providing a graphical interface to many of QEMU’s advanced options.

### Advanced features
You can save and restore QEMU VMs without any issues. It also supports the emulation of various architectures, from 32-bit machines to SPARC and PowerPC. Besides its impressive hardware virtualisation features, QEMU can also do user-mode emulation to run apps created for one platform on an entirely different one.

### Native hardware support
QEMU VMs can interface with many types of physical hardware on the host, including audio interfaces and all types of USB devices. But this isn’t one of its strongest suits. Instead, you can use QEMU to emulate various kinds of peripherals for its wide range of supported architectures.

### Integration with the host OS
You can share folders from the host with the guest running inside QEMU, although you’ll have to mount them inside the guest manually. But that’s about all the integration you can expect, as there’s no support for sharing clipboards to copy and paste text or files between the virtual guest and the host.

### Overall
QEMU tips the scales in terms of advanced features, but barely registers on the usability scale. This is why it’s best suited for advanced virtualisation campaigners looking for flexibility.

![](img/fb76008333fb7aef815b136f9f1afe5f_81_3.png)

## VirtualBox
The kitchen-sink approach to features wins it many fans.

![](img/fb76008333fb7aef815b136f9f1afe5f_82_0.png)

- The virtual networking infrastructure that's available in VirtualBox is one of the virtualisation's most interesting features

### Usability
VirtualBox employs a brief wizard to get users to customise the essential elements of a VM. Post-creation, you can either power it on or tweak the settings for its virtual hardware. The VM settings window houses useful options such as the ability to manually select a paravirtualisation interface for the VM.

### Advanced features
The app is chock-full of features. It can take snapshots of VMs and clone them and you can also import and export virtual appliances with relative ease. VirtualBox can also do port forwarding to let you run servers inside a VM. However, for some of its advanced features, like disk image encryption, you need to rely on the proprietary extensions module.

### Native hardware support
Another area where VirtualBox shines. It supports pass-through mode for SSDs and optical disks and is one of the only options that lets apps inside the VM use the host's 3D hardware. Its USB support lets you access all kinds of peripherals on the host and you can run VMs with high resolutions and spread them over multiple monitors connected to the host.

### Integration with the host OS
With VirtualBox, you can share clipboard and folders that can be configured to mount automatically. Off note is its Seamless Mode in which you can run virtualised applications alongside the ones on the host desktop.

### Overall
With its unique blend of advanced features and user-friendliness, VirtualBox offers enough to satisfy both experienced and inexperienced users alike.

8

## Virt-manager
It's tough at the top, but Red Hat's offering has much to recommend it.

![](img/fb76008333fb7aef815b136f9f1afe5f_82_1.png)

- While virt-manager primarily creates KVM virtual machines, it can also manage Xen and LXC containers

### Usability
Virt-manager (or Virtual Machine Manager to give it its full title) uses a fairly intuitive wizard to create new virtual machines. The application covers enough ground to give the system tweakers ample room to personalise their VMs while using reasonable defaults to help the first timer sail through. The application's main interface displays a list of all the VMs and if one is running, it'll also display its live resource utilisation statistics.

### Advanced features
The Virt-manager application offers fine-grained control over some pieces of hardware, which will appeal to advanced users. It can clone VMs and migrate them from one host to another and you can also import a QEMU copy-on-write image.

### Native hardware support
Inside the VM, sound works out of the box and the display can scale to full-screen. The virtualisation also supports the ability to attach USB devices including removable drives, webcams and Bluetooth devices connected to the host, and all work inside the guest seamlessly without any issues.

### Integration with the host OS
You can copy and paste text between the VM and the host once you've installed spice-vdagent on the host as well as inside the guest VM. However, you can't move files in the same fashion and unlike VirtualBox, there are no extra guest additions or similar extensions that will enable such features.

### Overall
Virt-manager has all the commonly used features you'd want. These are exposed via an intuitive interface that make the app a charm to use, irrespective of the skill level of the user.

7

## Review
### Desktop virtualisers
#### In brief: compare and contrast our verdicts

| | GNOME Boxes | QEMU | VirtualBox | Virt-manager |
|---|---|---|---|---|
| Usability | Easy to use, but with limited options to customise the virtual hardware. 7 | Essentially a command line utility that first-timers can use via third-party graphical UIs. 5 | Uses a very approachable graphical interface that’ll appease all kinds of users. 8 | There’s barely a learning curve thanks to the intuitive VM creation wizard. 8 |
| Advanced features | Can’t manage to rival the leaders in terms of features, but covers the basics. 7 | The number of advanced features is one area where the maturity of QEMU shines through. 8 | There’s no dearth of features here, though some require the proprietary extensions. 8 | This will woo advanced users with its extensive controls over virtual hardware. 7 |
| Native hardware support | Boxes failed to connect any hardware on the host besides USB drives. 5 | The ability to interface with the host’s hardware is a clear weak spot for QEMU. 6 | Enables you to use all kinds of hardware attached to the host with ease. 8 | The commonly used peripherals on the host can also be used inside the VM. 8 |
| Integration with the host OS | Sound inside the VM and copy and paste work without any issues. 7 | QEMU doesn’t offer much in terms of integration besides the ability to share folders. 6 | Besides clipboard and folder sharing, the Seamless mode deserves praise. 8 | Integration is one of the few areas where Virt-manager offers limited functionality. 7 |
| Overall | If you use a GNOME desktop, it wouldn’t hurt to take Boxes for a spin. 6 | Don’t begin your virtualisation adventures with QEMU, but it’s something to aspire to. 6 | Manages to edge out the competition even without the closed source component. 8 | Virtually as good as VirtualBox but without the shadow of proprietary extensions. 7 |

## AND THE WINNER IS...
### VirtualBox
This is one of those group tests where the numbers are a little misleading. As per the ratings, VirtualBox manages to edge past Virt-manager. But if you use the Open Source edition of VirtualBox (sans the closed source extensions) you’ve got a real good battle on your hands. In several areas, like CLI support which is very useful for managing VMs from the terminal and provisioning machines from within scripts, virt-manager gives VirtualBox a run for its money. Then there’s customising the virtual hardware, which is a virt-manager specialty. For instance, in addition to the number of CPUs, virt-manager enables you to specify a CPU model for the guest from its large collection of supported models, from Pentium 3 and Opteron G5 to Haswell, Westmere and more. We’re also impressed by virt-manager being quite intuitive to use and scaling well, which makes it ideal for a large demographic.

However, after a few lacklustre updates, VirtualBox once again picked up its game by incorporating parallelisation features. VirtualBox also boosts impressive VM performance and is packed with features.

![](img/fb76008333fb7aef815b136f9f1afe5f_83_0.png)

The closed source extensions are a small price to pay for VirtualBox’s impressive features.

True, some of its really useful desktop-centric features depend on the closed source extension pack, but it’s a small price to pay from a pragmatic point of view.

That said, while VirtualBox takes the crown, we’d still advise readers to give virt-manager a shot. If it does everything you need from a desktop virtualiser, then there’s really no need for anything else. In that sense, even GNOME users shouldn’t bypass Boxes just because it’s a simulation application compared to the others – it probably does enough to meet most users’ requirements.

Mayank Sharma
