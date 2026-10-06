
# Running applications virtually with KVM and QEMU

As with Xen, Kernel-based Virtual Machine (KVM) virtualization requires a computer that has an Intel VT or AMD-V processor. KVM, however, is implemented using a loadable kernel module that works with the standard kernel, instead of using a special Xen kernel. QEMU (http://bellard.org/qemu/) is used to remotely run the guest operating systems.

Each virtual machine running under KVM is private, virtualized hardware provides you with access to local hard disks, network interface cards, and other hardware resources. Some of the requirements for beginning KVM virtualization are the same as they are for Xen:

- You need at least 256MB of RAM for each guest.
- For hard disk space, you probably need between 2GB and 3GB at least for each guest system (judging from an average-size Fedora desktop install).
- You need to have the GRUB bootloader installed.
- You need an Intel VT or AMD-V processor (the "Before Installing Xen" section for information on how to check for support).

Now, you want to install many of the same packages installed for Xen. From the Add/Install window you can search for and install all appropriate xen packages. In particular, the kvm and qemu packages to needed by Xen (such as virtual-manager).

Before proceeding, make sure that you booted to the regular kernel and not the Xen kernel (if the xen packages are installed, both a regular and xen kernel should be available for you to boot). Then run the following procedure to install a new guest operating system that will run using KVM and QEMU:

1. **Start libvirtd** — If it's not already running, start the libvirtd service:

```
service libvirtd start
```

2. **Start KVM guest-install** — As root from a Terminal window, type the following:

```
# /usr/sbin/virt-manager
```

The Virtual Machine Manager appears.

3. **Create new guest** — Right-click localhost (qemu) and click New. When the Create a new virtual system pop-up appears, click Forward. You are asked to make your virtual system.

4. **Virtual machine** — Type a name to represent this virtual machine and click Forward. Keep the name simple (one word, fairly short, and no special characters) because the name is used to represent the virtual machine in file names and menus. You are asked the virtualization method.

5. **Visualization method** — Choose Fully Virtualized. You can also choose to create a guest that uses a different CPU architecture (i686, X86_64, ppc, sparc, mipsels). You are asked to identify the location of the installation media.

6. **Installation media** — Type the type of ISO image (you can browse for it) or the CD or DVD that has your installation media (such as a Fedora DVD) inserted. Also identify the type (generic, Linux, UNIX, Windows, or other) and variant (Fedora, Windows, Sun Solaris, for example) of the operating system you are installing. You are asked to assign storage space.

7. **Assign storage space** — You can identify a disk partition or create a virtual disk by identifying a name and size. In each case, the storage area must be large enough to hold your installed guest operating system. You are asked to set up a network connection.

8. **Host network** — Identify either a virtual or shared physical network device to provide connectivity for your guest operating system. Next allocate memory and CPU.

9. **Allocate memory** — From the total memory on the screen, choose the amount of VM to use and the maximum amount. At least 256MB is recommended. Also choose the number of CPUs to start with (typically less than the host system). You are asked to review your installation information.

10. **Start installation** — If all the information is correct, click Finish to begin the process. At this point, you will run through the installation process normally for the selected operating system. Once installation is complete, you can start and shutdown the new virtual environment from Virtual Machine Manager.

## Summary

Between applications written for Linux and other UNIX systems, those that have been ported to Linux, and those that run in emulation, thousands of applications are available. With the merging of Fedora Core and Fedora Extras online repositories, the number of high-quality software available to run on Fedora and RHEL has grown exponentially. To simplify the process of installing and managing Linux applications, Red Hat Package Management (RPM) format. Using tools developed for RPM such as yum command, you can easily install, remove, and perform queries on Linux packages. The types of applications that can run in DOS, Windows 95/98/2000/NT/XP/Vista, and Macintosh provide the greatest level of compatibility when used in Linux. In the long run, virtualization software such as Xen and KVM allow multiple operating systems to run as guests on Fedora, in turn.

## Chapter 6: Publishing with Fedora and RHEL

In This Chapter

- Desktop publishing in Linux
- Trying graphical text editors
- Using OpenOffice.org
- Creating documents with Groff and LaTeX
- Creating DocBook documents
- Displaying documents with Ghostscript and Acrobat
- Doing page layout with Libre
- Working with graphics
- Using scanners driven by SANE
- Publishing on the Web

To serve as a desktop system, operating system must be able to perform at least one task well: produce documents. Fedora and RHEL include tools for producing documents, manipulating images, and printing. This chapter describes Linux office suites such as OpenOffice and KOffice for creating presentations and spreadsheets. For page layouts, Libre is an excellent application that can be used to create brochures and pamphlets. For working with images, we cover the GNU Image Manipulation Program (GIMP). For working with vector graphics, we describe the Inkscape vector graphics editor. For displaying the content you create, there are several different viewers available for displaying output in PDF and PostScript formats. For PDF, there are the Evince viewer and Adobe Reader. To display PostScript files, there is Ghostview.

## Part II: Using Fedora and RHEL

If you want to publish on the Web, there are tools for writing basic HTML documents making Web sites with full-blown content management systems. Software that is packaged for Linux to manage your Web sites includes MediaWiki (wiki), WordPress (blogging), Drupal (content management), and Gallery (photo).

## Desktop Publishing in Linux

Whether you are writing a letter, a memo, or a book, you usually begin with a word processor. If your computer doesn't have much power, you might start with a simple text editor or a word processor as AbiWord. Most Linux users, however, begin with OpenOffice Writer. If all you need is to edit a plain text document, however, you can begin with a simple text editor.

## Using Text Editors and Notpads

Before jumping into more word processors, here are a few applications you might try out if you want to write some text quickly:

- **GNOME Text Editor (gedit)** — From the GNOME desktop, select Applications -> Accessories -> Text Editor. With the window that opens, you can just type, copy, and paste, and use arrow keys to move around. Besides creating text documents, edit has spell check and search tools. Highlight Mode (select View -> Highlight Mode), causes different parts of the text you are writing like code (such as C or Java) or markup (as HTML or XML) to be displayed in different colors.
- **KDE Text Editor (kwrite)** — From the KDE desktop, the KWrite application is the default text editor. KWrite includes many of the text editing features, but also has features and support for multiple language input.
- **Sticky Notes (tomboy)** — Different note taking applications KNotes (for KDE) and Tomboy (for GNOME). Tomboy puts a notepad in your top panel, from which you can create and manage notes. Create a new note that includes URLs (click to open in a browser) and links to other notes. Spelling is checked as you type. Organize notes in notebooks or do keyword searches to find the note you want.

If you want to move text from your plain text files or sticky notes to a more formal document, you can copy or cut, then the text into one of the word processors described in the next section.

## Using Word Processors

OpenOffice.org is a powerful open-source office suite available as part of the Fedora and RHEL distributions. Based on the Sun Microsystems StarOffice productivity suite, OpenOffice includes a word processor, spreadsheet, presentation manager, and other personal productivity tools. In many cases, OpenOffice.org can act as a drop-in replacement
