# # INTRODUCTION

This chapter starts by providing a list of Samba tools followed by some basic information. The JumpStart section discusses how to set up a Samba server using **system-config-samba**, a minimal GUI. The next section covers how to use **swat**, a Web-based advanced configuration tool, to set up a Samba server. The final server section discusses how to set up a Samba server by hand, using a text editor to manually edit the files that control Samba. The next two sections, "Accessing Linux Shares from Windows" (page 765) and "Accessing Windows Shares from Linux" (page 766), explain how to work with Linux and Windows files and printers. The final section of the chapter, "Troubleshooting" (page 768), offers tips on what to do when you have a problem setting up or using Samba.

Table 23-1 lists the utilities and daemons that make up the Samba suite of programs.

**Table 23-1 Samba utilities and daemons**
| **Utility or daemon** | **Function** |
| net | This utility has the same syntax as the DOS net command and, over time, will eventually replace other Samba utilities such as smbpasswd. |
| nmbd | The NetBIOS (page 1095) nameserver program, run as a daemon by default. Provides NetBIOS over IP naming services for Samba clients. Also provides browsing (as in the Windows Network Neighborhood or My Network Places view) support. |
| nmblookup | Makes NetBIOS (page 1095) name queries (page 769). |
| smbclient | Displays shares on a Samba server such as a Windows machine (page 767). |
| smbd | The Samba program, run as a daemon by default. Provides file and print services for Samba clients. |
| smbpasswd | Changes Windows NT password hashes on Samba and Windows NT servers (page 752). |
| smbstatus | Displays information about current smbd connections. |
| smbtree | Displays a hierarchic diagram of available shares (page 766). |
| swat | Samba Web Administration Tool. A graphical editor for the smb.conf file (page 755). |
| testparm | Checks syntax of the smb.conf file (page 768). |