
## Set up a secure VPS

![image](img/b6e789f7b1bc6629f6c97a3e4beae1de_15_0.png)

### Stay thy LAMP stack-installing hand a moment while we give you a primer on virtual private server security.

Virtual servers are cheap. In fact, with a few usage provisos, you can get one from Amazon for free and having your own virtual server is a great way to learn about all the responsibilities, pitfalls and street credits associated with remotely administering your own internet-facing box, without having to worry about failing hardware and hefty server bills.

Except for Amazon’s free usage tier, the cheapest virtual machines (VMs) out there run on what’s known as operating system-level virtualisation technology. The most abundant example is OpenVZ (Open Virtuozzo), which runs a modified Linux kernel that’s shared among all the guest OSes (OpenVZ only supports Linux guests, but why would you want anything else?).

> "Hypervisor relates to the fact that operating systems were once referred to as supervisors."

OpenVZ is close to being an example of a hosted (Type 2) hypervisor, since it runs inside a conventional OS. However, purists would argue that it doesn’t really do true virtualisation, but rather containerisation – being more akin to supervising a bunch of chroot environments rather than actual OSes. Incidentally, the etymology behind the word hypervisor relates to the fact that operating systems were once referred to as ‘supervisors’. Hence, a hypervisor is a supervisor of supervisors.

If you require a greater level of guest isolation, then you should direct your attention towards a bare metal (or Type 1) hypervisor, such as VMware or Xen. This model enables your guest OSes to run their own kernels, so you can run whatever you like. The hypervisor itself is fairly minimal and handles all the low-level hardware shenanigans.

In order to be of any use to guest OSes, a control domain (dom0) needs to be running on top of the hypervisor. This is a privileged VM running a Xen-enabled kernel which manages all the lesser guests (unprivileged domains) and provides an interface for them to interact with hardware. The Linux kernel supports Xen, but one can also use NetBSD or OpenSolaris as the control stack. We should also mention KVM here, which does an excellent job of obscuring the boundary between Type 1 and Type 2. Once the KVM module is loaded, the host OS becomes a hypervisor: a virtualiser, such as Qemu can then utilise it to run any OS compatible with the host’s CPU architecture. In fact, Qemu can virtualise x86, PowerPC and S/390 guests, but there’s a performance cost when emulating foreign architectures. Guests fall into two camps:

- Paravirtualisation (PV)
  - This requires a PV-aware kernel, so the guest knows that it’s running on imaginary hardware.
- Hardware-assisted Virtualisation (HVM)
  - Paravirtualisation’s counterpart, HVM – or full virtualisation – requires a CPU with virtualisation extensions which mitigates the performance penalty associated with tricking the Guest OS by emulating BIOS and other hardware. To further complicate matters, fully virtualised guests can be partially paravirtualised through so-called PV-on-HVM drivers, so that I/O can be accelerated and grey areas introduced.

Whatever path you go down, after a quick and easy credit card payment you will be provided with a hostname/IP address and password. You will then be able to ssh into your new appliance with full root access:

```bash
$ ssh root@host
```

There are a few initial things you should take care of, just as when you install a new OS on an actual machine. Some of these might be already done for you – it depends on the amount of effort put into whatever image you’re using. So you should check `/etc/hostname`, `/etc/locale.gen`, `/etc/hosts` (etc) and set up your timezone. It’s sometimes best to set this to UTC as it befits the virtual nature of the whole affair:

```bash
$ ln -sf /usr/share/zoneinfo/UTC /etc/localtime
```

> Elliptic Curve Crypto is so advanced that you can get away with much shorter key lengths (256, 384 and 521 bits versus 1,024, 2,048, 3,072 or 4,096 for RSA).

Now you should set up a normal user, as being root all the time is not a particularly good idea:

```bash
$ useradd -m -G wheel user
```

Replace `user` with your preferred handle. Here we have added ourselves to the `wheel` group, which lets us use `su` to become root. If you would rather use `sudo`, then the `-G wheel` part is not necessary – instead you will need to use `visudo`.

### Securing Secure Shell

Although you might have a good memory and a secure password, it’s preferable to go one step further and create a keypair to authenticate with ssh and disable password logins altogether. The public key is stored on the server and you should keep your private key somewhere safe and ideally not make any copies of it. If you do lose it, most VPSes will allow you to log in through a serial console and fix things. You can generate the keypair on your local machine by running:

```bash
$ ssh-keygen
```

You will be prompted for a filename for the private key, and then again for a passphrase. If you envisage having lots of different keys for many different servers, then it’s a good idea to change the default filename to include the relevant hostname. Otherwise, the default `~/.ssh/id_rsa` is probably fine. The public key will be generated in the same place with a `.pub` suffix. Note the pretty random art image associated with the key: these can be useful if you find yourself comparing keys at any point. By default, `ssh-keygen` produces a 2,048-bit RSA keypair which should be fine for all but the most paranoid. There are plenty of options though, so you could also make a 521-bit Elliptic Curve pair with:

```bash
$ ssh-keygen -t ecdsa -b 521
```

You then copy the key to your server with:

> “Qemu can virtualise x86, PowerPC and S/390, but there’s a performance cost.”

![image](img/b6e789f7b1bc6629f6c97a3e4beae1de_16_0.png)

### Disclaimer

Cheap VPS servers are definitely not a good idea for conducting any mission-critical operations or storing any data that is remotely sensitive. In this guide we do some rudimentary hardening, but this won’t make you bulletproof. Sound advice is to not run services you don’t need/understand and update everything regularly. Almost by design, there will always be some room for mischief. There are attack vectors outside of the VM itself: a kernel-level exploit on an OpenVZ setup could compromise any virtual machine running there, or there may be a vulnerability inside your hosting provider’s control panel – or any of their infrastructure for that matter.

Be aware, also, that there are many fly-by-night types operating in this budget sector, often overselling appliances through many layers of resellers. Some of them have fancy websites, but do not be deceived. Find some reviews and remember the old adage: if something sounds too good to be true, then it probably is.

And don’t expect much help either. You have to do reinstalls and reboots yourself through cPanel or (for the more impecunious) SolusVM. Although most providers have a ticket system for technical support, this is usually only for help at the hardware and OS image levels. Don’t expect them to tell you why your PHP script is running slowly or how to set up Apache.
