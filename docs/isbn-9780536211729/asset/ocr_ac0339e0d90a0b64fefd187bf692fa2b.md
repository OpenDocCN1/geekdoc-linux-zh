To determine the correct file, note the major and minor device numbers that represent listed, probably major:03 minor:01 if your root file system is on /dev/sda, or major:08 minor:01 if it is on /dev/sda1. In this case, the correct file is the one in the root file system, for example the one whose first pathname component is not of a mounted file system. Note that this worrying about the inode number and device is required if you are running an ancient pre-2.2 kernel.

Seeing "Cracker's Running Processes" on page 466 and "Handling Cracker Processes" on page 467 for details on what to do. You want to attempt to gather data on the running processes before shutting the system down and running a known good of Linux to start the recovery process.

# 8.23 Detecting Defaced Web Pages Automatically

Now, you have secured your Web server tighter than the FBI and CIA (both of their sites have been broken into), you have set up your firewall, and you have programs to scan the log files for suspicious entries. Have you done yet? The numbers for known Web site defacements are shown in Table 8.1. They show this process continuing to increase rapidly. The estimate for 2000 is mine and I very conservatively multiplied the numbers for January through April three, which does not allow for a clearly increasing condition.

Table 8.1 Web Defacements (per year)

| Year | Defacements* |
| 1997 | 40 |
| 1998 | 244 |
| 1999 | 3736 |
| 2000 | 4881 (est.) 5822 (actual) |

> *The Attrition organization monitors Web defacements. This table is excerpted from www.attrition.org/mirror/attrition/os.html

Many large and well-known sites get defaced and remain in that state for hours or longer because no one notices the problem. This is because most sites do not monitor their Web pages for alterations. Crackers enjoy the publicity and SysAdmins have discovered the problem when they get the pay in the morning. Some companies will be happy to monitor your site for a fee. One Web site advocates updating the Web pages from another system every hour. This leaves a 59-minute window and you will not know if the site has been defaced (cracked). Worse, a smart cracker will notice the modification times (crates) of the pages and simply deface the pages minutes after the SysAdmin has updated the pages. If a cracker manages to intercept communication upstream from the Web server, this hourly update scheme will fail completely because it will not be the server itself that was cracked.