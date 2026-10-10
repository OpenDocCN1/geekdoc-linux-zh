
strong password, and have the password manager generate (and remember) hard-to-crack, gibberish passwords for all the sites you use. There are plenty of cross-platform solutions that work through browser extensions and mobile apps, but there’s a few that actually support desktop Linux too. Our favourite is KeePassXC (https://keepassxc.org), which is a fork of the largely unmaintained KeePassX, which itself was a fork of the Windows-centric KeePass. You can install an older (but still good) version straight from the Ubuntu repos with:

```
sudo apt install keepassxc
```

Or use a snap to get a newer version with:

```
sudo snap install keepassxc
```

Then fire it up from the Applications menu and click ‘Create new database’. The default encryption and storage options are fine for normal humans, but feel free to turn everything up to 11. The next screen is the most important: it’s where you must decide your master passphrase. Choose wisely, and consider writing it down somewhere and keeping it somewhere safe, but not somewhere it’s likely to get stolen. Choose a location for your password database, and consider backing up this file (and all your important files) regularly. Now add your many, many freshly secured passwords. You can sort them into groups, and install the KeePassXC browser extension for Firefox.

## A matter of factor

Many services now offer two-factor authentication (2FA), where besides a password some other token is required. Often this second factor is an SMS message, but there are problems with this. For one, a determined attacker may have the means to carry out a SIM-swap attack, whereby mobile network staff are socially engineered (or bribed or blackmailed) into porting the victim’s phone number to an attacker’s sim. Mobile malware is becoming more and more prevalent (don’t install apps you don’t trust!) and if the victim’s phone has fallen victim to such then their SMS messages will all be up for grabs. The SS7 protocol that connects cellular networks has long been a source of concern for the security conscious. Once you have access to any cellular network – whether that’s internally through a rogue employee or externally by some devious hackery – it’s actually possible to access any other network and intercept or reroute messages as befits your whim. So using SMS as a second factor is certainly stronger than using no second factor at all, but other factors should be used for critical services. Hardware tokens and security keys are becoming much more widely supported as a second factor for popular services. The Challenge-Response card readers required by some forms of internet banking are an example; they add credence to the notion that it is the account holder trying to make a given transaction by proving that whoever is doing so has their card and PIN number. Unfortunately, these devices tend to spend most of their time getting lost or running out of battery at the most inopportune moments.

> ![](img/3f314b57ad3c8b08d25e5d1ab47de56d_66_0.png)
> Generate unwieldy passwords without worrying about having to remember them.

> GitHub supports 2FA. First set it up to use Google Authenticator, then you can use a U2F token.

### WE SECOND THIS MOTION

Google’s Authenticator app for Android is a software 2FA solution, albeit a proprietary one, that uses the Time-based One-time Password protocol (TOTP) to generate six- to eight-digit one-time codes for use as a second factor. It’s widely supported, not just on Google sites, so if you have an Android phone this is a free way to boost your security and reduce the chance of unfortunate takeovers. The magic of this is that, once a token is generated and shared between the site and the app, the same code is generated independently based on the current time. The algorithm can tolerate clock skews and network latency, so the app and the site don’t need to both keep exactly the same time. Authenticator codes can theoretically be spied on and, though an attacker would have to be watching you in real time for this to work, so for ultimate security we recommend using a hardware solution such as one of Yubico’s YubiKey range. These support a variety of authentication protocols. It can work in tandem with a TOTP app as a Universal Second Factor (U2F), or it can authenticate with supported services via NFC (Near Field Communication) on a mobile phone. It can also work as an unlock key for a password manager service. Which is nice.

> ![](img/3f314b57ad3c8b08d25e5d1ab47de56d_66_2.png)
> Yubico kindly sent us some YubiKeys – we’ll check them out in a future issue.

## VIRTUALISE ALL THE THINGS

Fed up with breaking Linux installs, and Linux installs breaking him, **Jonni Bidwell** looks to virtualisation to ease his very real woes.

> ![](img/3f314b57ad3c8b08d25e5d1ab47de56d_67_0.png)

- Without virtualisation, life at Linux Format towers would be a lot more complicated.
- Testing DVDs would be a nightmare, reviewing new distros would require us to wipe the machine on which we installed previous distros, and if we wanted to test new software on different distros, we’d probably need yet more hardware and yet more time.
- Yet if you rewind back to the late Mesolithic LXF age – the early 2000s – these were exactly the kind of hardware logistics that the team had to wrangle, all the while living the wild lifestyle encouraged by the heady golden era of dead-tree publishing. Back then tech journalists were made of stronger stuff.
- Nowadays things are much more straightforward. If you want to try a new OS, or even if you just want to do something a bit crazy with your current one, all you need do is fire up a virtual machine, and within minutes you have a device that for all intents and purposes behaves like a regular computer.
- Only you don’t need to worry about breaking it – anything you do can be undone, and no one will come at you with pointed questions/sticks if it breaks.
- For beginners, a virtual machine is a great way to try Linux. You can run VirtualBox for free on Windows or macOS. If you’re already running Linux you may prefer to use Red Hat’s Virtual Machine Manager, which uses QEMU (an emulator) and KVM (Linux’s powerhouse of a hypervisor) behind the scenes.
- Whatever your tastes, we’ve got something for you.

## Virtualisation 101

Nobody can tell you what virtualisation is – you have to experience it for yourself. Or you could just read this...

Virtualisation has been around since the 1960s. Of course, computing then was all done on mainframes and OSEs were a lot different, so it's harder for youngsters to get their trendy heads around how this worked. The idea then is essentially the same as it is now: compute resources were to be shared (fairly) amongst users in such a way that concurrently running jobs would not interfere with one another. Operating system kernels used to be called 'supervisors', and each separate job was more or less its own entity (today we expect our OSEs to multitask programs as a matter of course, but this wasn't the case back then). So the underlying OS which governed these jobs was referred to as a hypervisor, a term still used today.

> ![](img/3f314b57ad3c8b08d25e5d1ab47de56d_68_0.png)
> We use only virtual penguins to test our disc now – ever since that ugly uprising six years ago.

Modern hypervisors such as Xen and Microsoft's Hyper-V are thin OSEs that run on bare metal with the sole purpose of hosting guest VMs strictly and securely, much like the time-sharing scheme of the mainframe days. These are called Type-1 hypervisors, which correctly implies the existence of Type-2 hypervisors. The latter, exemplified by VirtualBox, Parallels and QEMU run on a regular operating system and are probably more familiar to everyday users. Things are not binary, though; Linux's KVM (Kernel-based Virtual Machine) doesn't fit nicely into either category, since it turns the kernel into something like a Type-1 hypervisor, but the host OSE still runs as intended.

In 2006, Intel and AMD started shipping processors with, respectively, VT-x and AMD-V extensions. These enabled operating systems to run virtualised without modification, in contrast to previous approaches such as paravirtualisation (which modified the OS to run in a guest environment) or complex software workarounds. Since then, virtually (ahem) all desktop CPUs have shipped with these hardware virtualisation extensions. And they have evolved to enable not only faster virtualisation, but deeper too, with hardware interrupts, memory management units (MMUs) and onboard graphics – via Intel's iGGT-G on Iris Pro graphics – now being virtualisable. It's even possible to blur the boundaries between physical and virtual: actual hardware can be handed off to a virtual machine and used seamlessly. A popular example of this is running a Windows 10 VM with a second (usually high spec) graphics card. This trick, known as PCIE passthrough, enables Linux users to play AAA games at very close to native speeds. PCIe and the general area of Virtual Function I/O (VFIO) require different CPU extensions, called VT-d on Intel and AMD-Vi on AMD. Some of Intel's overlocker-focused chips (the ones ending in K) lack these. One new project worth keeping an eye on is Looking Glass (https://lookeg-glass.hostingwindow.com) which aims to streamline passthrough setup for Windows VMs. In particular, the need for a separate monitor and keyboard is obviated.

### VIRTUALISATION, EMULATION AND CONTAINERISATION

It's easy to confuse virtualisation and emulation. Both are a piece of software masquerading as a machine, and both have been around for a long time. In one sense virtualisation is just a special form of emulation. On Linux, we can emulate lots of hardware; for example, a Raspberry Pi with QEMU, an Amiga with UME, or a Sega Megadrive with BlastEm (we know, we can emulate software using DOSBox or Wine (we know, Wine isn't an emulator – ah'et us) for example.

Emulation recreates everything in software, translating or rearranging foreign code into something the host can understand. Virtualisation differs in that the guest code runs directly on the host, which means it's faster (although sometimes other hardware still has to be emulated which makes it slower again), but also means it's only possible to virtualise architectures that are similar. Around a decade after the virtualisation revolution, a new technology emerged: containers. These were popularised by Docker in 2013 and bring many of the benefits of virtualisation (isolation, efficiency), but use the host's kernel, obviating the need to run a whole guest operating system.

Containers can be seen as OS-level virtualisation, as opposed to machine-level. Since a container need contain only the libraries required to run a particular application, they are eminently portable. They also provide a neat solution if that application only works with a particular version of a library. In the same way that Quebes OS runs applications in different VMs, OSEs like Container OS (formerly CoreOS Linux) and RancherOS run everything in containers.
