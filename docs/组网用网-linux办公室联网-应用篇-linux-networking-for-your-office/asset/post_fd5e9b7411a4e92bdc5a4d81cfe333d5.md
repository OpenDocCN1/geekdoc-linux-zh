
- Try another ISP—Sometimes one ISP has poorer lines than another, or hardware that doesn't interface as well with your modem as another's. Free trial periods can be a great way to test this.
- Replace your modem—Modems vary both in overall quality and in how well they cope with specific types of line defects.
- Service the phone line—Problems can sometimes be traced to weak telephone connections. I once had problems with poor connection speeds, retrains, and disconnections after rainfall. Water was seeping into the phone company's equipment outside my apartment and causing static on the lines.

You might also be the victim of an inactivity or usage timer. This comes part and parcel with the dial-on-demand solution, of course, but you can adjust the timing by editing the /usr/lib/diald/filter file, as described earlier in the chapter. It's possible to set such timers locally even if you're not using diald, however, and you might have inadvertently set such an option, particularly if you used a script or GUI tool you found on the Internet. ISPs sometimes implement similar limits on their end, especially during peak hours.

## Note

People occasionally post, asking for advice on getting around ISP-imposed inactivity timers. It's a trivial matter to set up a cron job that performs some minor Internet traffic at a set interval, but I strongly recommend against such a procedure. Some ISPs consider an attempt to remain connected when you're not using the computer a violation of their fair use policies, and might terminate your account. Even if that doesn't happen, always-on access drives up the cost to ISPs, who must then pass it on to their customers, most of whom don't abuse the system in this way. If you want always-on Internet access, you would be well advised to look into either a dedicated PPP account (one that's sold expressly for this purpose) or an alternative means of access, such as a DSL line, cable modem, or ISDN. DSL and cable connections, in particular, work just like ordinary Ethernet connections from Linux's point of view, and in many metropolitan areas, the price is comparable to that of a dedicated phone line and PPP account, with substantially faster access speeds.

## Summary

PPP over telephone lines has been a common method of providing Internet access to individuals and small businesses for several years, and it will likely remain common for several more years. This chapter describes how to set up a PPP link, including the necessary kernel drivers, serial port tests, and PPP configuration itself.

This chapter covers three different ways to start a PPP link: using manually run scripts, the X-ISP GUI dialer, and the diald dial-on-demand dialer. Each method has strengths and its weaknesses, so you can pick whichever of these best suits your specific needs.

Setting up a PPP link, using any method, can be a troublesome experience. Problems include difficulties with driver configuration, failures in authentication, and physical defects in the telephone system. Identifying and correcting these problems can be tricky, but this chapter presents some tips to help you in this task.

## File Sharing

## PART
III

## IN THIS PART

- 9 Basic Principles of File Sharing 215
- 10 NFS: Sharing Files with Other UNIXes 241
- 11 Samba: Sharing Files with DOS, Windows, and OS/2 255
- 12 Netatalk: Sharing Files with Macintoshes 291
- 13 Using Linux to Back Up Client Machines 315

## Basic Principles of File Sharing

## CHAPTER
9

## IN THIS CHAPTER

- Using Mount Points Effectively 216
- Understanding Ownership and Permissions 223
- Case-Sensitivity in Linux and Other OSs 230
- Serving Removable Media 231
- Security Considerations 237
- Summary 239

Linux is one of the best operating systems in existence when it comes to file sharing over a network. This is because Linux offers flexibility in two areas: network filesystems and disk-based filesystems. Red Hat Linux supports, out of the box, the Network File System (NFS) protocol for file sharing with UNIX computers; Samba, for file sharing with DOS, Windows, and OS/2 computers; and NetWare Core Protocol (NCP), for file sharing with NetWare computers. With an additional package (included on the CD-ROM that accompanies this book), Red Hat supports AppleTalk, for file sharing with Macintoshes. This range of support, although not unparalleled, makes Linux quite flexible, and you’ll be hard-pressed to find an operating system (OS) with more choices.

Similarly, Linux supports a plethora of disk-based filesystems, including its own native ext2fs; various options for the File Allocation Table (FAT) variants used by DOS, Windows, and OS/2; Windows NT’s NT File System (NTFS); OS/2’s High-Performance File System (HPFS); Macintosh’s Hierarchical File System (HFS); the ISO-9660 and Joliet filesystems used on CD-ROMs; UNIX File System (UFS) for various UNIX flavors; and still other more exotic systems. Of course, if you’re using a Linux box to serve files stored locally, this unusually wide range of support isn’t terribly important. Linux allows you to share removable media, though, which could potentially contain any of these filesystems. You can also install a hard disk that had previously been used in another OS and directly share its files, or use this support as a stopgap measure when converting a server from another OS or if you need to dual-boot the machine.

No matter what network or local filesystems you use, though, there are certain concepts with which you must be familiar before you can get the most out of any file-sharing configuration. This is especially true if you’re most familiar with Windows or MacOS because Linux’s handling of files and filesystems is different from the way these OSs handle them in ways that are both obvious and subtle. Therefore, the goal of this chapter is to introduce important concepts, both of file sharing in general and of Linux’s handling of files, particularly as this handling interacts with file sharing with DOS, Windows, OS/2, and Macintosh clients.

## Using Mount Points Effectively

In order to understand Linux file-sharing practices, it’s important to know something about Linux’s partitioning and filesystem philosophy. In general, Linux file sharing is less dependant on partitioning than is file sharing under OSs, such as Windows. Linux also provides ways to access files in an area that’s not explicitly exported, which can be both a great convenience and a potential security concern.
