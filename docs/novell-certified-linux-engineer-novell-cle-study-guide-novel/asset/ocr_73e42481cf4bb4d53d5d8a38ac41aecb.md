# CHAPTER 5 NNLS Installation and Administration

The first task you must complete to start the NNLS installation process is to obtain a copy of the product. The manner in which NNLS is distributed is a bit different from other software products on the market today. You can't run down to your local computer store and buy a copy off the shelf.

NNLS is distributed only through the Internet. To obtain a copy, you must visit http://www.novell.com or the website of an Authorized Novell Reseller. On these sites you will find a link that allows you to purchase a copy of the product.

When you execute the purchase, you will receive an email containing links where NNLS can be downloaded. There are three separate items you need to make sure you receive:

+   > **NNLS 1.0 CD**—You should see a link that allows you to download a copy of NNLS version 1.0. The file you will receive is an ISO image. An ISO image is a file that contains a complete image of an ISO 9660 compact disc (CD). Be aware that this ISO image file contains the full contents of the NNLS CD. It will be a very large download—over 300MB, so don't even think about trying to do it with a modem or you will likely be entering retirement when the download completes. Even with a 256Kbps DSL connection, it will still take the better part of the day to download.

+   > **NNLS 1.0 Companion CD**—Your email should also contain a link to download a second ISO image for the NNLS 1.0 Companion CD. As with the NNLS ISO image, this file is very large and you should not try to download it with a modem. It contains the Novell GroupWise Collaboration Client for Windows, the Novell NetDrive client for Windows, and DirXML drivers (discussed later in the course).

+   > **A Novell International Cryptographic Infrastructure (NICE) key file**—Your email message should also contain a link that allows you to download a NICI file (\*.nfk) required by eDirectory. This file is actually quite small (only a few KB) and is not distributed as an ISO image. Simply copy this file to a floppy disk. During the NNLS installation process, the installation routine will look for this file on the floppy disk mounted in /media/floppy (or in /mnt/floppy on a Red Hat system).

Once you've downloaded your ISO images, you need to decide how you want to use them to install NNLS. You have two options, the first of which is to use a CD burner to burn the ISO image to disc. This is a point of confusion for many. When I say, "burn the ISO image to disc," I'm not referring to putting the ISO image file itself on the CD. Instead, we mean using your