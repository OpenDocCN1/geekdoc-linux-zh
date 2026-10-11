
## RETENTION METHOD FOR APPLICATION LOG

Configuring the retention method for security logs enables you to determine how events are overwritten. You have three options: you can overwrite events by day, you can overwrite events only as needed, or you can choose not to overwrite events at all. If you choose the last option, then you will be forced to manually clear the log. The most efficient setting in most circumstances is to overwrite events as needed. This ensures that you do not overwrite more events than necessary, but still allows the Event Log to create needed room.

![](img/763d5ae436311371600c0952a3da9094_580_0.png)

![](img/763d5ae436311371600c0952a3da9094_580_1.png)

- 1. Expand the Security Settings container, expand the Event Log container, then select Settings For Event Log.
  - The policy settings appear in the details pane.
- 2. Double-click the Retention Method For Application Log policy setting.
- 3. The Retention Method For Application Log policy window appears.
  - Click the check box to either enable or disable the policy setting.
- 4. Click either the Enabled or Disabled radio button.
- 5. Click OK.

# APPENDIX A

## RETENTION METHOD FOR SECURITY LOG

You can also configure the retention method for Application, Security, and System logs. These policies allow you to determine how events are overwritten. You have the option of overwriting events by day, as needed, or not overwrite events. If you choose not to overwrite events, then you must clear the log manually. In most circumstances, the most efficient setting is to overwrite events as needed. This allows the Event Log to create room but does not overwrite any more events than necessary.

- 1. Expand the Security Settings container, expand the Event Log container, then select Policies For Event Logs.
- 2. Double-click the Retention Method For Security Log policy setting.
- 3. The Retention Method For Security Log policy window appears.
- 4. Click the check box to either enable or disable the policy setting.
- 5. Click either the Enabled or Disabled radio button.
- 6. Click OK.

![](img/763d5ae436311371600c0952a3da9094_581_0.png)

![](img/763d5ae436311371600c0952a3da9094_581_1.png)

## SHUTTING DOWN THE COMPUTER WHEN THE SECURITY AUDIT LOG IS FULL

You have the option to automatically shut the computer down when the Security Audit log is full. This option can be used in cases where you do not want data overwritten and the computer has reached its maximum size. The computer will shut itself down, then an administrator can view the log before clearing it. Obviously, this is not an option you want to use on a regular basis.

![](img/763d5ae436311371600c0952a3da9094_582_0.png)

- 3. Click the check box to either enable or disable the policy setting.
  - The Shut Down the Computer When The Security Audit Log Is Full policy window appears.
- 4. Click either the Enabled or Disabled radio button.
- 5. Click OK.

559

# APPENDIX B

## WHAT'S ON THE CD-ROM

The CD-ROM found at the back of this book contains several resources you may find valuable. First, the entire text of this book, including all screen captures is available in .pdf format so you can read the book and search for topics electronically. As you work with the Active Directory and need to reference information from time to time, you will find the electronic version of this book very useful. The CD-ROM also includes several other items that either fall under the category of “demos” or “utilities.” The following two sections tell you what is available in each.

### System Requirements

Make sure that your computer meets the following minimum system requirements. If your computer doesn’t match up to most of these requirements, you may have problems using the contents of the CD.

- A PC with a Pentium II 300 MHz or faster processor.
- Microsoft Windows 2000 or Windows 98 with Internet Explorer 5 or later.
- At least 64MB of total RAM installed on your computer.
- At least 10 MB of hard drive space available to install all the software from this CD. (You need less space if you don’t install every program.)
- A CD-ROM drive — double-speed (2x) or faster.
- A monitor capable of displaying at least 256 colors or grayscale.
- Visual C++ 6.0 with service pack 3 installed.

### A word about Shareware et al.

Shareware programs are fully functional, free-trial versions of copyrighted programs. If you prefer a particular program, then register with that program’s author, pay a nominal fee, and receive licenses, enhanced versions, and technical support for the program. Freeware programs are free, copyrighted games, applications, and utilities. You can copy freeware programs — for free — to as many PCs as you like, but be aware that freeware programs usually have no technical support. GNU software is governed by a General Public License (GPL), which is included inside the folder of the GNU software. The only restriction for using or distributing GNU software is a big one — you can’t restrict anyone else’s use of the GNU software. (See the GPL for more details.) Trials, demos, or evaluation versions are usually limited, either by time (30 days from installation, for example) or functionality (such as not being able to print or save your projects).

After examining these products, you may wish to purchase them to aid you with your Active Directory and Windows 2000 implementation.

### DirectMigrate 2000

Demo version. DirectMigrate 2000, by Entevo Corp., is a tool that assists you in migrating objects from other LDAP directories into the Active Directory. This tool can be very useful if you are moving from an environment such as Novell Directory Service (NDS) to the Active Directory. DirectMigrate can also assist you in migrating Windows NT resources to the Active Directory and even enables you to test your migrations before running them. To learn more, visit www.entevo.com.

### DirectAdmin

Demo version. DirectAdmin, also by Entevo Corp., contains a number of capabilities to help Active Directory administrators. DirectAdmin can help you create, update, rename, and delete Active Directory objects and properties. DirectAdmin supports cross-platform functionality and enables you to perform many Windows 2000 functions more easily, as well as manage the Active Directory. To purchase DirectAdmin or to learn more, visit www.entevo.com.

![](img/763d5ae436311371600c0952a3da9094_583_0.png)

### Micro House Technical Library

Evaluation version. Micro House Technical Library contains a wealth of information about various technical topics that you can search. Micro House Technical Library is a useful asset for both learning and troubleshooting. A trial version of the library is available on the CD-ROM for your review. To purchase the product or to learn more, visit www.microhouse.com.

### WS_FTP Pro

Trial version. WS_FTP Pro, by Ipswitch, is a file transfer utility for use with Windows operating systems. You can use WS_FTP Pro to manage FTP directories and perform uploads or downloads of FTP files. WS_FTP Pro on the CD-ROM is a trial version you can examine for possible use in your environment. To purchase WS_FTP Pro, visit www.ipswitch.com.

### MindSpring Internet Access

MindSpring Internet Access is a commercial product that gets you signed up to the MindSpring Internet service provider. If you don’t already have Internet access, MindSpring is an excellent ISP that offers Internet access for a low monthly fee. MindSpring also has different Web hosting options depending on the kind of account you have. If you’re already on the Internet but would like to learn more about MindSpring and the different service options it offers, you can visit the Web site at www.mindspring.com.

**IMPORTANT NOTE:** If you already have an Internet service provider, installing MindSpring may replace your current settings. You may no longer be able to access the Internet through your original provider.

Also note, if you already have Internet Explorer 4.0 or later installed on your computer, select the Custom Install option when you install MindSpring Internet Access, and deselect Internet Explorer. This will prevent MindSpring from attempting to replace your browser with an earlier version.

### Utilities

The following shareware utilities are also available on the CD-ROM for your use.

### Diskeeper Lite for Windows NT

Diskeeper Lite For Windows NT is freeware included on the CD-ROM for your use. Diskeeper Lite provides you with a high-speed, manual defragmentation utility used to defragment hard disks on Windows NT 4.0 computers. Because disk defragmentation is not offered in the operating system, Diskeeper Lite is a necessary and useful utility.

### IP Subnet Calculator

Commercial Product. As you plan your Active Directory implementation, you may be faced with planning an IP subnet. The IP Calculator included on the CD-ROM can help you easily calculate digital-to-binary conversions and can be a very useful tool for use with tricky TCP/IP configurations.
