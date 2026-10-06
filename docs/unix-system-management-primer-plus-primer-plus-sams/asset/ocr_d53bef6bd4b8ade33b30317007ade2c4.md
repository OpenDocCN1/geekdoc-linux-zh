# Chapter 3 • DEPLOYING YOUR SYSTEMS 71

system over the network rather than using a CD-ROM. This information might be important if you later find out about a bug on the CD-ROM or some other critical factor. You should consider logging the following information about OS software:

+   - Versions and patch level of operating systems installed on each server
- Installation procedures for each operating system, including any problems you encountered and their workarounds
- Additional software installed on a system that is not covered by your standard installation procedures
- Configuration changes you made after installation

Be sure to keep this information up-to-date so others can maintain your systems if you are not available.

# Installing from a CD-ROM

The most common installation mechanism is via CD-ROM. A CD-ROM installation is a fairly straightforward process for operating systems, usually as inserting the disc into the drive and powering on the server. For applications, most Unix distributions will automatically mount a CD-ROM you insert into a local file system, and you install the application by running a script in that file system.

There are three requirements for CD-ROM installations:

+   - Media on CD-ROM
- A CD-ROM drive
- For operating system installs, firmware (BIOS or equivalent) support for booting from CD-ROM

![](bbox=[0.118, 0.626, 0.178, 0.672])

# CD-ROM Speed

CD-ROM installations used to be painfully slow with old single- and double-speed drives in the mid1990s, but now with 24x-, 32x-, and even 48x-speed drives, CD-ROM drive speed is no longer a factor.

Installing an operating system from CD-ROM can be difficult because it requires the insertion of a disc into each system being loaded. The only way to automate a CD install is to use a separate disc for each system. Unfortunately, media costs and copy protection may prohibit this solution, especially if the OS installation requires more than one disc. For applications, usually only the file system on the CD-ROM is necessary—you can copy the contents of the disc onto a file system and copy it to another server or share it with all of your servers. See the section titled “Installing from the Network” later in this chapter for more details.