# Pen testing

![](bbox=[0.05, 0.15, 0.17, 0.25])

# Use VDI technology for a pen-testing training setup

Virtual desktop infrastructure frameworks are great tools for ethical hacking of real (or simulated) systems

# Toni Castillo Girona

has a bachelor's degree in software engineering and an MSc in Computer Security and works as an ICT research support expert in a university. You can read his blog at: disabuxes.upc.es

# Resources

+   *   RAVADA VDI
+       https://ravada.upc.edu/index.html
+   *   Libvirt
+       https://libvirt.org
+   *   KVM
+       https://www.linux-kvm.org/page/Main_Page
+   *   SPICE
+       https://www.spice-space.org
+   *   Installing Ravada VDI on Debian
+       http://bit.ly/RAVADAVDI
+   *   Libvirt Network Filters
+       http://bit.ly/libvirt
+   *   Web Security Dojo 3.0
+       http://bit.ly/WebDojo

This tutorial has been tested on a Debian Jessie 64-bit box

We are all quite acquainted with the concept of the three As regarding access to information (or ATAWAD): any time, anywhere and from any device. Virtual Desktop Infrastructure (VDI) is just a manifestation of such a promise: nowadays it would seem pointless to have a whole computer classroom with separate images deployed on every single box. We are all living in the era of the cloud, after all. Enter VDI. But, of course, this is not the only use we can find for VDI technology. Pen-testing, malware analysis and forensics are also well-known scenarios where a VDI broker can save the day! RAVADA VDI is one such VDI framework, ready to install and use. Its back-end has been designed and implemented in order to allow future hypervisors to be added to the framework, thanks to its REST API. This is great because you don't need to worry too much about KVM falling off a cliff some day: RAVADA VDI will certainly support the trendy hypervisor of the future. Deploying this framework will help you design and manage pen-testing training scenarios where you will be able to test any crazy, out-of-the-ordinary proof of concepts (PoCs) without damaging a single system.

As of this writing, RAVADA VDI only supports the KVM hypervisor, which means you need to load the proper module for your kernel. So, if you have an Intel-based processor, run (as root): `modprobe kvm-intel`. For AMD-based processors, run: `modprobe kvm-amd`.

From an end-user's point of view, the only requisites are a web browser and a remote viewer supporting the SPICE protocol (for example, `apt-get install virt-viewer`).

# Nested KVM

You can set up the framework on a computer with nested KVM capabilities. This way you can try RAVADA VDI before deploying it. You can create a new VM using libvirt and its vir-manager tool and then install RAVADA VDI on that VM. Make sure your processor does support nested KVM first: `cat /sys/module/kvm_intel/parameters/nested`. An output of 'Y' or '1' means you are good to go. If you don't have nested KVM capabilities, don't panic: there's still a chance you can have them: unload the kvm module and then reload it with the `nested=1` parameter:

```
modprobe kvm-intel nested=1
```

# Install and use RAVADA VDI on Debian

If you want to use this VDI broker on Debian Jessie, you need to make some changes first (see Resources). Note that RAVADA VDI is yet to be tested on Debian Stretch, which was released on 17 June.

Clone the repository and start looking at its nuts and bolts. The code is written in Perl 5 and AngularJS. The development team behind RAVADA VDI has implemented a bunch of tests to make sure everything is in order

![](bbox=[0.2, 0.68, 0.85, 0.89])

Above An easy-to-use GUI framework is essential to any modern VDI framework; RAVADA VDI uses Mojolicious to that end