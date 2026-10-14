
## MAKING YOUR MAIL TOP SECRET

Internet email is about as secure as sending a postcard—any postal clerks along the delivery path can read your message if they wanted to since there's no envelope to protect it. So if you're concerned about your private email falling into the wrong hands, encryption is the solution.

Encryption will scramble your message so that only the holder of the secret decryption key will be able to read it. The de facto standard for encryption is the PGP (Pretty Good Privacy) program, written by Phil Zimmerman. Actually pretty good privacy is a pretty serious understatement. If you use a sufficiently long password key, the computing power required to crack the code that PGP uses becomes astronomically large.

## ARE YOU A CRYPTO CRIMINAL?

PGP is such a good program that the United States government has classified it as a "munition" and made exporting it illegal, for reasons of national security. Apparently the feds are worried that the bad guys will be able to correspond in a way they can't decode. Although it is not illegal to send a message that has been encoded by PGP, you can't export (via email, FTP, or any other means) the PGP software from the United States, except to Canada (or from Canada, except to the United States), without a license from the federal government. The one strange exception to this rule is that printed books containing the PGP source code can be exported.

It is also illegal to use PGP in some countries (it's legal in the United States), so if you are an evil terrorist or are plotting the overthrow of your government, check with your local authorities first before using PGP. The Crypto Law Survey at http://cwis.kub.nl/~frw/people/koops/lawsurvy.htm summarizes the legalities of PGP around the world.

## GETTING PGP

If you're interested in learning more about PGP, see the PGP FAQ at http://www.cam.ac.uk/pgp.net/pgpnet/pgp-faq/ on the Web.

To get a copy of the PGP software, visit http://web.mit.edu/network/pgp-form.html to see the PGP Distribution Authorization Form. If you are a citizen of the United States or Canada and promise to use it for noncommercial purposes and never export it to any other countries, you can download the Unix source code for PGP, which you will have to compile yourself. If you plan to use PGP for commercial use, you can purchase it from Network Associates, at http://www.nai.com.

## COMPRESSION, ENCODING, AND ENCRYPTION UNDER DOS

If you're working on a DOS system and you come across a tar file, a gzip file, or a file that has been uuencoded, all is not lost. Fortunately, you can find DOS tools for dealing with compressed and encoded files at a variety of sites on the Internet, and most of them are free.

Visit http://www.shareware.com or http://www.download.com and use the search engines there to find DOS or Windows versions of tar, gzip, uuencode, and PGP. The Wincode and WinZip shareware programs are very popular, so you might want to try them first.

![](img/3137cdda7122042e86dbeafe9840d4ed_289_0.png)

## LINUX DOES DOS AND WINDOWS

- Accessing DOS Floppies with MTOOLS 260
- Accessing DOS Partitions with MOUNT 262
- Running DOS Programs with DOSemu 263
- Running Windows Programs with Wine 268
- Running VMware: Industrial-Strength Virtual Windows 271
- More Linux Compatibility Tools 272

Even though Linux is a very complete operating system, you will probably have occasion to access the programs and files you left behind in the DOS world. Fortunately, there are several ways to do so without shutting down Linux and booting up DOS.

This chapter will show you how to use the MTOOLS package to read and write DOS floppy disks under Linux, and how to mount your DOS hard drive partition to access a DOS file system while running Linux. You'll also learn about DOSemu, a DOS emulator that runs under Linux, as well as WINE, a Windows emulator that enables you to run Microsoft Windows applications in Linux's X Windows environment.

## ACCESSING DOS FLOPPYIES WITH MTOOLS

Do you need to list the files on a DOS-formatted floppy disk while running Linux? Do you need to copy a file from a DOS disk to your Linux file system, or vice versa? You can use the MTOOLS commands to do these and lots of other DOS-like things with Linux.

The MTOOLS package is a set of Linux commands that mimic the DOS commands DIR, COPY, TYPE, DEL, RENAME, and a few others. They're called the MTOOLS because they all start with the letter m, and they work much like their DOS counterparts.

Here's a list of the MTOOLS commands and what they do:

- mattrib Modify the attributes of a file.
- mcd Change the current directory.
- mcopy Copy a file.
- mdel Delete a file.
- mdir List the files in the directory.
- mformat Format a disk.
- mlabel Change the disk label.
- mmd Make a new directory.
- mrd Remove a directory.
- mren Rename a file.
- mtype Display the contents of a file.
