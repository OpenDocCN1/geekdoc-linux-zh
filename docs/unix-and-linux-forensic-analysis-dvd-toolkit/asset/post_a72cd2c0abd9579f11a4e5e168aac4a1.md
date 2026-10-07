
# Bootable nix ISOs

There are several different bootable Linux OSes which can be used for persistent data acquisition. They can be used on either a *ix or Windows platform, as they are completely self contained within the CD, and are designed to never touch the resident file system.

The most popular of these types of systems are:

- HELIX^5
- Knoppix^6
- BackTrack 2^7
- Penguin Sleuth^8
- INSERT^9

When a bootable OS would be depends on the situation. If for some reason a resident version of Linux is not available on the forensic system, any one of them can be used locally, or within VMware session. The same holds on the target. If the investigator feels more comfortable with a Linux-based system, or if for reason your normal attempts at Windows image acquisition has failed, any of these OSes can be used. As stated earlier, one of the key components to being prepared is to have multiple tools in the forensic toolbox can be used to gather data. The key is to test them all in a laboratory environment to ensure that troubleshooting the OS does not take place at the customer location.

The following section provides a high level overview of each of the bootable OSes provided, as well as any special functions that the investigator may need to know to acquire a dd image.

## Helix

Helix 1.9a is a Knoppix-based system running a 2.6.14-Kanotix-9 Linux kernel. When HELIX begins the boot process, the user will be prompted for which version they would like to start. For the purposes of this paper, "GUI" has been selected. The system will boot into the default XFACE 4.2.3.2 desktop.

> 5 www.e-fense.com/helix/
> 6 www.knopper.net/knoppix-mirrors/index-en.html
> 7 www.livedistro.org/release-announcements/gnu/linux-releases/backtrack
> 8 http://penguinsleuth.org/index.php?option=com_wrapper&Itemid=39
> 9 www.inside-security.de/insert_en.html

The default behavior for Helix is to populate the GUI desktop with icons representing each volume it detects during boot. By default, clicking on these will mount them as read. To utilize for any evidence gathering, the forensic investigator can issue the mount command with the remount option, "mount -o remount,rw /media/sdb1".

Helix comes preloaded with several good forensic and incident response programs, which have also been statically linked to the CD. The forensic tools, which can be used to acquire images, Adepto, Air, LinEN, and Retriever. Forensic Analysis tools, which can be used to view the contents of the images as well as perform different search functions, Autopsy, pyflag, regviewer, hexeditor, xff diff, and xhfs. Incident response tools include Ethereal (now called Wireshark), Clam Anti-Virus scanner, and F-prot Anti-Virus scanner.

The steps for acquiring an image with Helix are no different than those which would be used during the standard Linux imaging process. One important point to remember about the kernel of any Linux release, is that it does not like the New Technology File System (NTFS). For obvious reasons, the drivers used for NTFS support are sketchy at best and should not be trusted. When using an external drive for image storage, remember to format the drive with either the EXT2 or EXT3 file system. The process for this is described in the “Prepare the Target Media” section of this paper.

## Knoppix

Knoppix is the “mother” of all bootable Linux OSes. It has been around the longest, wonderfully supported and maintained by Klaus Knopper, and even has several books written about it. Knoppix is not a security or forensic Linux release, but a fully functioning OS, which includes Web browsers, OpenOffice, games and graphics editing capabilities.

Version 5.1.1 to the KDE desktop, and on Linux kernel 2.6.19. It is user friendly and well-documented; however, it does not contain any forensic, incident report, or security centric tools. It loads as if you were running a default installation of a Linux OS. This should be taken into consideration when choosing this release.

Being a current Linux kernel, it comes loaded with all of the standard Linux utilities, so like Helix, the process for mounting a drive and dd'ing an image would be the same if you booted into a resident Linux OS.

![](img/fd8e85097b37559dbc07dc22fd8cb1fe_68_0.png)

Even with the current kernel and the requisite drivers for NTFS support, caution should be used when writing to an NTFS partition. If the case that is being worked could end up in litigation, the ext2 or ext3 file system should be used on the target media. A knowledgeable defense attorney will know that the drivers are not good, and could easily bring your evidence under scrutiny by the jury.

## BackTrack 2

According to the BackTrack2 homepage,10 “BackTrack is the most top rated linux distribution focused on penetration testing. With no installation whatsoever, the analysis platform is started directly from the CD and is fully accessible within minutes.

It evolved from the merge of the two widespread distributions Whax and Auditor Security Collection. By joining forces and replacing these distributions, the BackTrack could gain a massive popularity and was voted #1 in 2006 at insecure.org. Security professionals as well as newcomers are it as their favorite toolket all over the. New exciting features in BackTrack include:

- Updated kernel 2.6.20
- Broadcom-based wireless
- Metasploit framework
- Redesigned menu
- Japanese input
- Ability to burn CDs
- Boot via network or USB drive

Even with the current kernel and the requisite drivers for NTFS support, caution should be used when writing to an NTFS partition. If the case that is being worked could end up in litigation, the ext2 or ext3 file system should be used on the target media. A knowledgeable defense attorney will know that the drivers are not good, and could easily bring your evidence under scrutiny by the jury.

## INSERT

Inside Security Rescue Tool (INSERT) is built on the 2.6.18.5 Linux kernel, boots to a GUI that displays the documentation. This is a great feature and is the only one of the bootable OSes mentioned that actually provides you with documentation on start-up. INSERT is broken into sections including network analysis, data recovery, virus scanning, computer forensics. All of which are available by right-clicking anywhere on the desktop and making a selection.

According to the documentation, INSERT has NTFS support using the latest ntfs drivers. The documentation on the Web page provides a comprehensive testing methodology, as well as results and testimonials. INSERT also provides the user with the option of downloading and installing applications as Mozilla's Fire, and running them from RAM.

## EnCase LinEn

EnCase for Linux (LinEn) was added to EnCase version 5. It is similar to the DOS version of EnCase, which includes all the benefits of the more powerful and flexible Linux tools.(It is worth noting that the EnCase DOS version no longer exists as of the release of version 6. If using to acquire in Windows, it is also available to have the same version of linen running as the EnCase forensic version.) Before you begin with this acquisition method, there are a few housekeeping steps that need to be taken of. First, copy the LinEn binary onto the media you intend to use as your target media. Remember, Linux does not work with the NTFS file system.
