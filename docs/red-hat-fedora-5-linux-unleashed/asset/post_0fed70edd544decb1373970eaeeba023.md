
The Personal Desktop installation requires nearly 2GB of hard drive space but should easily fit onto smaller hard drives in older Pentium-class PCs. The install also contains administrative tools, additional authoring and publishing clients, a variety of editors, a GNOME-based X11 desktop, support for sound, graphics editing programs, and graphical and text-based internet tools. You can customize the selection to include or sidestep installation of unwanted software. See Chapter 3 for details.

Connecting to the Internet is a snap, and Fedora supports modem dialup and other broadband connections, such as cable modems or digital subscriber line (DSL). See Chapter 18, “Network Connectivity,” for more information. When you do connect, you can do so in relative confidence because firewall protection from malicious intruders and other attackers can be thwarted by running the lokkit or system-config-securitylevel clients. Chapter 18 also explains how to set up a local network.

If you have a digital camera, run the gphoto2 client to download, organize, and manage your digital images. You can then fine-tune your pictures by editing them using one of the finest digital image editors in the world: The GIMP. See Chapter 10, “Multimedia Applications,” for details on editing graphics.

Fedora can be used for a variety of purposes, and every user has different needs. Some of them might be esoteric. For example, I use Fedora to program and manage thousands of frequencies on various radio scanners and amateur radio transceivers, run a high-frequency shortwave radio via a graphical interface on the desktop, host wireless (802.11 a/h/g) printing for several workstations, manage digital recording of my favorite TV episodes, provide secure remote access via a firewall, and listen to my favorite music playlists via a server.

## 64-Bit Fedora

Recent advances in computing saw the introduction of 64-bit x86-compatible CPUs from AMD in the spring of 2003. The only platform at launch to support the new technology was Linux, and, even at the time of writing, it is still the only mainstream operating system actively using the power of the 64-bit x86 architecture. Intel’s EM64T extensions for x86, which largely mirror the advances made by AMD, have further increased the availability of commodity x86-64 hardware.

As a direct response to the growing 64-bit user base, The Fedora Project released an x86_64 version of Fedora Core 2, allowing the use of Fedora on AMD64 and Intel hardware. If you have a 64-bit CPU, you are strongly encouraged to get involved and have a go—just bear in mind that, because the architecture is still quite new, there might not be 64-bit versions of all the software you require.

However, because the Intel Itanium platform uses a radically different set of instructions that are not compatible with the x86 instruction set, the 64-bit version of Fedora does not support Itanium or Itanium2. There are members of the community who are working toward making the Itanium a supported platform, but the niche nature of the platform means that this is unlikely.

## Fedora on the PPC Platform

In recognition of the wide availability of the Power architecture, The Fedora Project decided to simultaneously release a PPC version of Fedora starting with Fedora Core 4. Fedora Core 5 continues in this vein, and now you are able to run Fedora natively on Apple hardware such as PowerMacs, iMacs, and the Mac mini, not to mention the very tasty PowerBooks.

Of course, now that Apple has moved across to Intel processors, it has left a large gap in the Power market. Vendors such as IBM and Genesi will still produce and in IBM’s case, develop the PowerPC platform beyond the current crop of G4- and G5-based machines.

## Fedora on Dual-Core Machines

The second half of 2005 brought significant availability of dual-core processors from Intel, AMD, and Power. As always, Linux was at the forefront of support for new computing platforms and dual-core processors were no different. Fedora natively supports dual-core, and significant speed enhancements can be had from using such machines. Thankfully they are widely available in both the desktop and server environment.

## Getting the Most of Fedora and Linux Documentation

Nearly all commercial Linux distributions include shrink-wrapped manuals and documentation covering installation and configuration. You will not find official documentation included on the DVD provided with this book. However, you can read or get copies of assorted manuals or topic discussions online at http://fedorora.redhat.com/projects/docs/. There you will find The Fedora Project’s links to various documentation projects.

You can also turn to Red Hat’s official manuals and guides, particularly for Red Hat Linux 9, for interim information about Red Hat tools (such as those listed in Table 1.1) at http://www.redhat.com/docs/manuals/linux/RHL-9-Manual/. Note that the names that began with redhat-config in Red Hat Linux 9 now begin with system-config in Fedora.

Documentation for Fedora (and many Linux software packages) is distributed and available in a variety of formats. Some guides are available in Portable Document Format (PDF) and can be read using Adobe’s Acrobat Reader for Linux or the evince client. Guides are also available as bundled HTML files for reading with a web browser such as links, KDE’s Konqueror, GNOME’s Epiphany, or Firefox. Along with these guides, Red Hat provides various tips, frequently asked questions (FAQs), and HOWTO documents.

You will find traditional Linux software package documentation, such as manual pages, under the /usr/share/man directory, with documentation for each installed software package under /usr/share/doc.

Linux manual pages are compressed text files containing succinct information about how to use a program. Each manual page generally provides a short summary of a command’s use, a synopsis of command-line options, an explanation of the command’s purpose, potential caveats or bugs, the name of the author, and a list of related configuration files and programs.

For example, you can learn how to read manual pages by using the man command to display its own manual page like so:

```
$ man man
```

After you press Enter, you see a page of text appear on the screen or in your window on the desktop. You can then scroll through the information using your keyboard's cursor keys, read, and then press the Q key to quit reading. More information about using the command line can be found in Chapter 5, "First Steps with Fedora."

Many of the software packages also include separate documents known as HOWTOs that contain information regarding specific subjects or software.

If the HOWTO documents are simple text files in compressed form (with filenames ending in .gz), you can easily read the document by using the zless command, which is a text pager that allows you to scroll back and forth through documents (use the less command to read plain-text files). You can start the command by using less, followed by the complete directory specification and name of the file, or pathname, like this:

```
$ less /usr/share/doc/httpd-2.0.50/README
```

To read a compressed version of this file, use the zless command in the same way:

```
$ zless /usr/share/doc/attr-2.4.1/CHANGES.gz
```

After you press Enter, you can scroll through the document using your cursor keys. Press the Q key to quit.

If the HOWTO document is in HTML format, you can simply read the information using a web browser, such as Firefox. Or if you are reading from a console, you can use the links or lynx text-only web browsers, like this:

```
$ links /usr/share/doc/stunnel-4.0.5/stunnel.html
```

The links browser offers drop-down menus, accessed by clicking at the top of the screen. You can also press the Q key to quit.

If the documentation is in PostScript format (with filenames ending in .ps), you can use the gv client to read or view the document like this:

```
$ gv /usr/share/doc/iproute2-2.4.7/ip-crefs.ps
```

Finally, if you want to read a document in Portable Document Format (with a filename ending in .pdf), use the xpdf client like this:

```
$ xpdf /usr/share/doc/xfig/xfig-howto.pdf
```
