# **daily\_local="**/etc/daily.local**"**

You can define your own scripts to be run as part of the daily, weekly, and monthly periodic(8) jobs. These default to `/etc/daily.local`, `/etc/weekly.local`, and `/etc/monthly.local`, but you can place them anywhere you like.

Each script in the daily, weekly, and monthly subdirectories of /etc/periodic has a brief description at the top of the file, and most have configuration options in `/etc/defaults/periodic.conf`. Skim through these quickly, looking for things that are of interest to you. The defaults enabled are sensible for most circumstances, but there's extra functionality you can enable with a simple setting in /etc/periodic.conf. For example, if you use GEOM-based disk features, you'll find the daily GEOM status messages useful. Since anything I could list here would be obsolete before I could deliver this manuscript, let alone before the book reaches you, I won't go into detail about the various scripts.

# **/etc/pf.conf, /etc/pf.os**

We cover the basics of the PF packet filter in Chapter 19.

One less-known feature of PF is its ability to identify operating systems by the packets they send. The /etc/pf.os file contains TCP fingerprints for different operating systems, allowing you to write firewall rules such as “Show FreeBSD users my real home page, but show Windows users a page suggesting that they get a real operating system.” See pf.os(5) for more information. I encourage you to peruse this file, if only to drive home how all these network stacks behave so differently.

# **/etc/phones**

Modem users can store phone numbers for remote modems in /etc/phones, aliasing them so that they can just type home instead of the full