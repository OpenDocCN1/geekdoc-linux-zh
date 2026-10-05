
Try some foreign letters and symbols:
\p \AA \o \O \l \L \ss \ae \OE \pounds \copyright \ddag S\n. There are also three dashes of different length: ---

Try some accents over the letter '`a': \`'(a) \^(a) \*\(a) \^(a) \-(a)\n={}(a) \b(a) \c(a) \d(a) \h(a) \t(a) \u(a) \v(a). Other letters can be accented in a similar way.

The pair of `''` marks a math context. Many special characters are available only in the `math` context. For example, try the Greek alphabet:

Small: $\alpha \beta \gamma \delta \epsilon \varpsilon \zeta \eta$
$\theta \vartheta \sigma \tau \iota \kappa \lambda \mu \nu \xi \o \varpi$
$\rho \omega \upsilon \tau \phi \varpi$
$\chi \psi \omega$

Capital: $A B \Gamma \Delta E Z H \Theta H I K \Lambda M \Xi \Pi P$
$\Sigma T \Upsilon \Phi X \Psi \Omega$

Try some equations: $x^{n}(y+1) + x^*(tq)=z_{\{try\scripts\}}$

```
\center
$\frac{x \times y}(x/2)=\frac{1}{3}$
\end{center}
```

LaTeX math commands are very similar to those in the old `Word Perfect` equation editor.

Use the verbatim to print the 10 special symbols which normally have special meaning in LaTeX: `\verb{\$\#^\~}`. The special symbols must be contained between two identical characters in which the example is |. Most of these special symbols can also be printed by preceding the character with a backslash: \% \_ \_ \# ^\~

% This command ends the document $ (this is the third one *must* be present in every document)
\end{document}

## 7.10 Writing CD-Rs (cdrecord and cdparanoia)

Disclaimer: Copying copyrighted material is illegal. Do NOT use the instructions below for anything illegal.

## INTRO

Setting up a CD writer can be tricky. For good info see the http://www.guug.de/~wenni/linux/cdr/html/CD-Writing-3.html.

I used the above document to set a cheap, no-name IDE-ATAPI CD writer on a PC running RH6.0. It works, and no changes to my setup were required after the recent upgrade to RH6.1.
Here are the steps I followed (almost everything to be done as root):

## SETUP

In the file /etc/lilo.conf add a line at the end of the Linux "image" section:

append="hdb=ide-scsi",

Adjust the line above if your CD writer is not "hdb" (second drive on the first IDE interface). It makes your IDE-ATAPI CD-W(R) to be seen on your Linux system as a SCSI device. (It is not really a SCSI device, it is an IDE device, it pretends to be SCSI.) Run lilo after making any changes to /etc/lilo.conf. The change above is necessary to be able to enable SCSI on IDE-ATAPI CD-R(W) if you use Linux kernel 2.2.x.

- Add the loop devices to the /dev/ directory. This is not an obligato, but a nice feature you can enjoy creating your own CDs. The loop device will let you mount a CD image (if it was already a filesystem) to inspect its content. The loop devices don't exist on my hard drive after Linux RedHat installation, so I create them:

```
cd /dev/
mknod loop
```

- Add two lines at the end of the file /etc/rc.d/rc.local so that the needed kernel modules are automatically loaded on system setup:

```
/sbin/insmod ide-scsi
/sbin/insmod loop
```

These two kernel modules are needed for SCSI emulation of IDE drives and to support the loop devices, respectively.

- Create or modify the device /dev/cdrom so it now points to the correct device, most likely:

```
ln -s /dev/sr0 /dev/cdrom
```

You need to do this because your "dev/cdrom" pointed to an IDE device (probably /dev/hdb) but now these changes your CD-R is going to SCSI emulation mode.

- Reboot the system for /etc/lilo.conf to take effect. Check if your CD-R(W) still works properly for normal reading.

- Download the "cdrecord" from your favorite Linux software repository (e.g., httpfdirect.linux.org/). Then install the source code, compile it, install the program, and make symbolic links that are easy to run (the installation would be much easier if you found a binary *.rpm file):

```
cd /usr/local
tar -xvzf /the_path_to_which_you_downloaded/cdrecord-1.6.1.tar.gz
ls
cd cdrecord-1.6.1
make
```

```
make install
ls /opt/schily/bin/
ln -s /opt/schily/bin/* /usr/local/

The program cdrecord is a spartan, command line utility for writing CD. There are several GUI front ends to it, but they will be useless if the underlying cdrecord does not.

- Check if your CD-R is in SCSI emulation mode.

- The program cdrecord is a spartan, command line utility for writing CD. 

```
cd /usr/local
tar -xvzf /the_path_to_which_you_downloaded/cdrecord-1.6.1.tar.gz
ls
cd cdrecord-1.6.1
make
```

```
make install
ls /opt/schily/bin/
ln -s /opt/schily/bin/* /usr/local/
```

The program cdrecord is a spartan, command line utility for writing CD. There are several GUI front ends to it, but they will be useless if the underlying cdrecord does not.

- Check if your CD-R is in SCSI emulation mode.

- The program cdrecord is a spartan, command line utility for writing CD. 

```
cd /usr/local
tar -xvzf /the_path_to_which_you_downloaded/cdrecord-1.6.1.tar.gz
ls
cd cdrecord-1.6.1
make
```

```
make install
ls /opt/schily/bin/
ln -s /opt/schily/bin/* /usr/local/
```

The program cdrecord is a spartan, command line utility for writing CD. There are several GUI front ends to it, but they will be useless if the underlying cdrecord does not.

- Check if your CD-R is in SCSI emulation mode.

- The program cdrecord is a spartan, command line utility for writing CD. 

```
cd /usr/local
tar -xvzf /the_path_to_which_you_downloaded/cdrecord-1.6.1.tar.gz
ls
cd cdrecord-1.6.1
make
```

```
make install
ls /opt/schily/bin/
ln -s /opt/schily/bin/* /usr/local/
```

The program cdrecord is a spartan, command line utility for writing CD. There are several GUI front ends to it, but they will be useless if the underlying cdrecord does not.

- Check if your CD-R is in SCSI emulation mode.

- Create a CD image containing:

```
mkisofs -o image.iso /path
```

- The mkisofs command creates an ISO9660 image.

- To burn the image to the CD:

```
cdrecord -dev=/dev/sr0 image.iso
```

## AUDIO CDs

- Audio tracks have to be in files of *.cdr (I guess it is the same as cdda.raw), *.wav, or *.au format before you can write them to a CD.
- The utility sox converts between the various file formats (sox converts quite a few of them). For example, this will convert a .wav file to a .cdr:

```
sox my_file.wav my_file.cdr
``` This is convenient because audio files tend to be large.

- CDs don't contain a filesystem, they store "raw data". This means you cannot mount an audio CD. Also, each track is written separately, i.e., as if it were a different "partition" on the CD.
- To read audio tracks from an audio CD and write them to a suitable file on your hard drive (typical format is *.raw or *.wav), you need a "cd ripper". A popular CD ripper is "cdparanoia". After downloading the source for cdparanoia, install it:

```
cd /usr/local
tar -xzf
/the_path_to_you_downloaded/cdparanoia-III-alpha9.6.src.tgz
ls
cd cdparanoia-III-alpha9.6
./configure
make
make install
```

The installation program places a proper link to the executable (/usr/local/bin/cdparanoia) so I don't have to create the link manually.

To rip the first track from an audio CD, I can use:
cdparanoia 1
