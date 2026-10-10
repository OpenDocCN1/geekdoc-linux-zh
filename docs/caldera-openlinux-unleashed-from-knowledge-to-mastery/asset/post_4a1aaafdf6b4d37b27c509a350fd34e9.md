
## FIGURE 24.1

A virtual private network.

![](img/df365d352a104b50fea29e59a052de4d_609_0.png)

In a virtual private network, all traffic across the Internet is encrypted by the transmitting gateway and decrypted by the receiving gateway. For example, to the hosts on the left part of the network in Figure 24.1, the hosts on the right part may appear simply as local hosts on the local network. The two gateways take care of encrypting the traffic that crosses the Internet.

The IP Secure (IPSec) standard specifies protocols for building virtual private networks across the Internet. A free VPN implementation for Linux is FreeS/WAN, whose home page is http://www.xs4all.nl/~freeswan/. Since the software was developed outside the U.S., it is freely exportable.

FreeS/WAN lets you set up two Linux machines to act as VPN gateways. It includes several encryption algorithms and supports public key encryption and standards for key exchange.

Unfortunately, FreeS/WAN requires modifications to the Linux kernel and (as of this writing) works reliably only with kernels in the 2.0 series. Setting it up is beyond the scope of this book; download the package and read the excellent documentation included with it if you are interested in setting up a VPN.

Another VPN option is PoTPoP, which provides a virtual private network compatible with Microsoft’s PPTP setup. PoTPoP does not require kernel modifications. Its home page is http://www.moretonbay.com/vpn/pptp.html.

There may be other tools available; check the “Tunneling” section on http://www.opensec.net.

## Summary

In this chapter, you have learned computer security basics, including a useful definition of a secure computer. You learned about the various components of security, including physical security, personnel security, and network security.

Next, you learned the UNIX security module, which provides unlimited permissions to the *root* account. You learned about common attacks on UNIX programs, including buffer overruns, network sniffing, social engineering, password guessing, and denial of service attacks.

After learning about attacks, you learned how to prevent them by using firewalls and limiting the use of SUID/SGID programs. You also learned how and what to monitor to detect intruders and how to control access to network services using the TCP Wrappers package.

Next, you learned about the importance of keeping your system up-to-date and were given some resources for learning about security problems and fixes.

Finally, you learned how to ensure a modicum of privacy over the Internet and how to obtain software to set up secure virtual private networks.

![](img/df365d352a104b50fea29e59a052de4d_610_0.png)

# Linux Applications

## Part III

### IN THIS PART

- 25 Using Productivity Software 577
- 26 MySQL Essentials 593
- 27 Using Image Manipulation Tools 615
- 28 Typesetting Documents 649
- 29 Setting up Sound and Multimedia 671

## CHAPTER 25

# Using Productivity Software

### IN THIS CHAPTER

- Using WordPerfect 578
- Using StarOffice 585

Caldera Open Linux 2.3 ships with many productivity packages—in fact, there are too many to cover in a single chapter. Just to get you started, we’ll take a look at two of them: WordPerfect, long considered the premier word processing package worldwide; and StarOffice, which combines word processing with spreadsheet, presentation, email, and other software into a first-class office suite.

After getting your feet wet with these two, you really should take the time to investigate some of the many other productivity software packages available, such as Plan and Korganizer (scheduling), Kaddressbook (contacts), and The Gimp (graphics). Variety is the spice of life, and it is definitely one of the many advantages to Linux computing.

## Using WordPerfect

WordPerfect, in its many incarnations and ownerships, has set the standard for word processing worldwide for more than a decade. Over the last few years, it has evolved into a virtual office suite all by itself, incorporating graphics manipulation and spreadsheet functions directly into document processing, while advanced layout features enable the production of handsome, professional-looking presentations.

### Installation

If you performed a recommended install using Lisa, or recommended plus commercial using Lizard, the main portion of WordPerfect is already installed. If not, mount your Caldera OpenLinux 2.3 CD-ROM, switch to the /OpenLinux/install/RPMS, and install using the following command:

```
rpm -ivh WordPerfect-8.0.7.1386.rpm
```

After the main portion of the install has finished, WordPerfect must be set up for individual use. You must log in as the user you are setting up for, and then run /usr/bin/xwp. At this point, you will be prompted for a serial number, which can be obtained by registering your software at http://venus.corel.com/nasapps/wp8linuxreg/register.html.

### Getting Started

While Corel WordPerfect 8 for Linux functions essentially the same as WordPerfect 8 for Windows, you will nevertheless notice an immediate difference when you first launch the Linux version: WordPerfect begins by opening a small program box that contains all your setup options (display, document locations, quick format, and so on) and also controls WordPerfect. From here, you can open multiple WordPerfect windows (referred to as *Windows* in this chapter) containing new or existing documents. Here you will also find a list of the most recently-opened documents (your current task list).

Be careful with those W!indows, though! They operate somewhat differently than you might expect. When you choose **Open** or **New** from the File menu in a W!indow, you are telling WordPerfect to open another document in this window, thus closing the document you have on your screen. In other words, the File menu options of a W!indow are replacement functions and will not open an additional W!indow. This is one of those things you'll learn after the fourth or fifth time you accidentally close the document on which you're working.

The other primary difference that experienced WordPerfect users will notice lies in the shortcut keys. Many of the shortcuts used in Windows versions of WordPerfect can have unexpected results in the X Windows environment, so some have been eliminated and others have been changed. It is wise to use the menu options until you become accustomed to the new shortcuts.

### File Management

To open an existing file, choose **Open** from the File menu of a W!window, or choose **Open Window** from the Program menu in the Program box (referred to in this chapter as simply *Program*).

To create a new document from scratch, choose **New** from the File menu of a W!window, or choose **New Window** from Program.

Remember that the work you do in a W!window is not permanently stored until you save it as a file. Use **File, Save** to save your work from time to time to prevent its loss in the event of a system failure.

> **Tip**
> 
> WordPerfect for Linux has the same automated backup function that other versions of WordPerfect use. From **Program, choose Preferences, Files** to set the location of your temporary backup files and the frequency of automated backups. This doesn't take the place of using **File, Save** every so often to preserve your work, but it does serve as an additional safeguard.

To save a file for the first time, choose **Save** from the File menu. Then place the cursor in the **Filename/Current Selection** text box, and type the new filename. Remember to check the path where you are saving the file. You can change directories by navigating in the **Directory List** section on the right. Finally click **OK**, and the file will be saved.

### Tip

Remember that Linux supports long filenames, which can be very handy—but only up to a point. If your filenames are too detailed, you'll still find yourself reading line after line of directory listings, trying to determine which file you're after. Develop abbreviations for certain document types (ltr for letter, env for envelope, lab for labels, and so on) that make searching easy, and utilize a good directory structure to organize your files just as you would in a filing cabinet.

To save the current document under a new name (if you're editing a form you want to preserve or aren't certain you want this new version to be “The Version”)), choose File, Save As and proceed as if you're saving a new file. Double-check that filename and path before clicking OK.

To save a file in a different file format, choose File, Save As and make a selection from the Save Options/File Format dropdown box. Specify a filename and path (you can use the current filename to replace the existing file or type in a new name to preserve the old format), and then choose OK to save the file under a new name and format.

Remember, use File, Save to save successive updates on an open document under the same filename, and use File, Save As to save the open document under a new name.

## Formatting Documents

Happily, page formatting is essentially the same in WordPerfect 8 for Linux as in other versions of WordPerfect and many other popular word processing programs. The following basics will get you started, and a bit of experimentation with various menu options will help you perfect your technique.

### Page Setup

Choose Format, Page for most of your basic page setup options: size and layout of page, numbering, and so on. Headers and Footers, however, are under the Insert menu.

Use Format, Margins to change the whitespace between the text and the edge of a printed page. The default settings for margins are 1 inch on all sides of the page.

To change your margins, move your cursor to the paragraph (for side margins) or page (for top or bottom margins) where you want to make a change, or select (with your mouse) the paragraphs for which you want to change the left or right margins, and choose File, Page Setup, Margins or choose Format, Margins. Next, specify new settings for Left, Right, Top, or Bottom margins and then click OK to activate the new settings.
