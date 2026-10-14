
![](img/39e65eeb4f54001ede08c6114ae3cc6c_64_0.png)

Figure 2-6: The main K3b CD-burning window.

![](img/39e65eeb4f54001ede08c6114ae3cc6c_64_1.png)

Figure 2-7: Using the Brasero utility to burn an ISO image file.

## Burning CDs in Windows

The Windows environment doesn't contain CD-burning software by default. Many free and commercial packages are available, but not all of them include an option for burning ISO image files.

If your particular CD-burning software package doesn't burn CD images, Ubuntu recommends a free CD image-burning software package called InfraRecorder. The InfraRecorder package can be found at the popular SourceForge web site (infrarecorder.sourceforge.net).

Just download the InfraRecorder package and install it on your PC. After you start InfraRecorder, click the Actions menu bar item, then select Burn Image. You’ll see a dialog box to select the image to burn, then another dialog box will appear (shown in Figure 2-8), waiting for you to insert a blank CD to start the burning.

![](img/39e65eeb4f54001ede08c6114ae3cc6c_65_0.png)

**Figure 2-8:** The InfraRecorder CD burning tool for Microsoft Windows.

Once you insert a blank CD, InfraRecorder burns the ISO image file onto it. After you have the LiveCD ISO image on a CD, it’s time to start playing around with Ubuntu!

## Booting the LiveCD

The beauty of the Ubuntu LiveCD is that it offers you a real taste of what running Ubuntu on your PC is like, without the hassle of going through the installation process. When you boot the LiveCD from your PC, Ubuntu goes through all of the normal boot processes as if it were actually installed on the PC hard drive. This includes detecting your PC hardware and trying to load the appropriate drivers (called modules in Linux) to interact with the detected hardware.

The following sections walk through the Ubuntu LiveCD boot process and how to use Ubuntu once you get it started from the LiveCD.

## The Boot Process

The first step in booting the LiveCD is to determine whether and how your PC can boot from its CD drive. Many PCs can do so by default. Just place the Ubuntu LiveCD in your CD tray and restart your PC. If your particular PC doesn’t boot from the CD, there are a couple of things you can try before giving up.

First, go into your PC BIOS and see whether it’s set to allow booting from the CD drive. Different PC motherboard manufacturers use different BIOS software, and there are a multitude of ways to configure this setting. Figure 2-9 shows the boot sequence section in a sample BIOS setup.

![](img/39e65eeb4f54001ede08c6114ae3cc6c_66_0.png)

Figure 2-9: The boot sequence BIOS settings.

Once you find the boot sequence section, ensure that the CD is higher up in the list than the hard drive. This forces the PC to check for a bootable CD before trying to boot from the hard drive.

Another trick that many PC manufacturers use is a hot key during the boot process to select the boot device. On some PCs, hitting the F12 key during the boot splash-screen brings up a boot menu, allowing the user to select which device to boot from. The user selects a CD/DVD device, and the system boots from the CD.

## Using Ubuntu

After you start the Ubuntu boot process, you should see the main Ubuntu boot screen, shown in Figure 2-10.

![](img/39e65eeb4f54001ede08c6114ae3cc6c_67_0.png)

Figure 2-10: The Ubuntu boot menu.

The LiveCD allows you to perform four functions other than booting Ubuntu:

- Install Ubuntu to the hard drive.
- Check the validity of the LiveCD.
- Test the memory on the PC.
- Boot from the PC’s hard drive.

The last option can be a lifesaver in an emergency. There may be a time when the boot sector on your hard drive becomes corrupt, and the Linux OS won’t boot. Just pop in your trusty Ubuntu LiveCD, select the option to boot from the hard drive, and you might be able to save your data!

If you choose to boot from the CD image, Ubuntu goes through all of the hardware detection processes as if it were booting from an installed image.

You’ll notice that you can access several options from the boot menu using the keyboard F keys. Table 2-1 shows what each of these keys are for.

## Table 2-1: The Ubuntu LiveCD Boot Menu Keys

| Key | Description |
|-----|-------------|
| F1 | Display a Help screen that lists the F key options. |
| F2 | Select the default language used for the Ubuntu menus. |
| F3 | Select the keyboard mapping used for Ubuntu. |
| F4 | Select the boot mode for video devices. |
| F5 | Enable special accessibility features, such as screen magnifiers or on-screen keyboards. |
| F6 | Provide additional boot parameters to the GRUB (boot loader) |
