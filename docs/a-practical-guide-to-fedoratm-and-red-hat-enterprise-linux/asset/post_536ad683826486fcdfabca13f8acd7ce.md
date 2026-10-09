
BitTorrent, like other P2P systems, does not use a dedicated server. Instead, the functions of a server are performed by the tracker, peers, and seeds. The *tracker* is a server that allows clients to communicate with each other. Each client—called a *peer* when it has downloaded part of the BitTorrent file and a *seed* after it has downloaded the entire BitTorrent file—acts as an additional source for the BitTorrent file. Peers and seeds are collectively called a *swarm*. As with a P2P network, a member of a swarm uploads to other clients the sections of the BitTorrent file it has already downloaded. There is nothing special about a seed: It can be removed at any time after the torrent is available for download from other seeds.

The first step in downloading a BitTorrent file is to locate or acquire the *torrent*, a file with the filename extension of *.torrent*. A torrent contains pertinent information (metadata) about the BitTorrent file to be downloaded, such as its size and the location of the tracker. You can obtain a torrent by accessing its URL, or you can acquire it via the Web, an email attachment, or other means. The BitTorrent client can then connect to the tracker to learn the locations of other members of the swarm it can download the BitTorrent file from.

After you have downloaded a BitTorrent file (the local system has become a seed), it is good manners to allow the local BitTorrent client to continue to run so peers (clients that have not downloaded the entire BitTorrent file) can upload *at least* as much information as you have downloaded.

## PREREQUISITES

Use *yum* (page 534) to install the *transmission-cli* package. Put the following lines in the */etc/sysctl.conf* file and reboot the system. Without these lines *transmission-cli* will work *more* slowly and display messages suggesting you add the lines to *sysctl.conf*.

```bash
$ cat /etc/sysctl.conf
net.core.rmem_max = 4194304
net.core.wmem_max = 1048576
```

### transmission-cli: Downloading a BitTorrent File

The following example shows *transmission-cli* (www.transmissionbt.com) downloading a Fedora DVD ISO image. (Visit torrent.fedoraproject.org for a list of Fedora torrents you can download.) Depending on the speed of the Internet connection and the number of seeds, downloading a large BitTorrent file can take from hours to days. A torrent can download one or more files; the torrent specifies the filename(s) for the downloaded file(s) and, in the case of a multifile torrent, a directory to hold the files. The torrent in the example saves the BitTorrent files in the *Fedora-19-x86_64-DVD* directory in the working directory.

With a torrent in the working directory, enter a command such as the following, substituting the name of the torrent you want to use for the Fedora torrent:

```bash
$ transmission-cli Fedora-19-x86_64-DVD.torrent
[15:20:29.914] Transmission 2.77 (14031) started
[15:20:29.915] RPC Server: Adding address to whitelist: 127.0.0.1
[15:20:29.916] DHT: Generating new id
[15:20:30.021] Saved "/home/sam/.config/transmission/torrents/Fedora-19-x86_64-DVD.687077ce9c5fe811.torrent"
[15:20:30.021] Fedora-19-x86_64-DVD: Queued for verification
[15:20:30.022] Fedora-19-x86_64-DVD: Verifying torrent
[15:20:30.248] Port Forwarding (NAT-PMP): inNatpmap succeeded (0)
[15:20:30.248] Port Forwarding (NAT-PMP): sendpublicaddressrequest succeeded (2) Progress: 0.0%, dl from 0 of 0 peers (0 kB/s), ul to 0 (0 kB/s) [None]
[15:20:38.258] Port Forwarding: State changed from "Not forwarded" to "Starting" Progress: 0.0%, dl from 0 of 14 peers (0 kB/s), ul to 0 (0 kB/s) [None]
[15:20:49.001] Fedora-19-x86_64-DVD: Starting IPv4 DHT announce (poor, 9 nodes) Progress: 1.1%, dl from 27 of 36 peers (2.45 MB/s), ul to 1 (123 kB/s) [0.03]
[15:21:23.137] DHT: Attempting bootstrap from dht.transmissionbt.com
[15:22:38.259] Port Forwarding: State changed from "Starting" to ":?:" Progress: 14.1%, dl from 28 of 35 peers (2.10 MB/s), ul to 2 (40 kB/s) [0.02]
```

The `transmission-cli` utility displays messages about what it is doing. The lines that include the word `Progress` show how much of the BitTorrent file `transmission-cli` has downloaded, the number of peers and the total download speed, the number of clients it is uploading to, and the upload speed.

You can abort the download by pressing `CONTROL-C`. The download will automatically resume from where it left off when you download the same torrent to the same location again.

### Make sure you have enough room to download the torrent

> **caution**
> Some torrents are huge. Make sure the partition you are working in has enough room to hold the BitTorrent file you are downloading.

See the `transmission-cli man` page for a list of options. One of the most useful options is `-u` (`--uploadlimit`), which limits how much bandwidth in kilobytes per second the swarm can use while uploading the torrent `from the local system` (upstream bandwidth). Use `-U` (`--nouploadlimit`) to place no limit on the bandwidth the swarm can use. The following command prevents BitTorrent from using more than 100 kilobytes per second of upstream bandwidth:

```bash
$ transmission-cli -u 100 Fedora-xxxxx.torrent
```

BitTorrent usually allows higher download rates for members of the swarm that upload more data, so it is to your advantage to increase this value if you have spare bandwidth. You need to leave enough free upstream bandwidth for the acknowledgment packets from your download to get through or the download will be very slow.

The name of the file or directory BitTorrent saves a file or files in is specified by the torrent. You can specify a different file or directory name by using the `--save-as` option. The `transmission-show` utility displays the name the BitTorrent file will be saved as, the size of the file, the name of the torrent (**metadata** file), and other information:

```bash
$ transmission-show Fedora-19-x86_64-DVD.torrent
Name: Fedora-19-x86_64-DVD
File: Fedora-19-x86_64-DVD.torrent

GENERAL
Name: Fedora-19-x86_64-DVD
Hash: 687077ec95f03111a0f7326e425a518bb76161c29
Created by:
Created on: Mon May 27 20:08:14 2013
Piece Count: 17113
Piece Size: 256.0 KiB
Total Size: 4.49 GB
Privacy: Public torrent

TRACKERS
Tier #1
http://torrent.fedoraproject.org:6969/announce

FILES
Fedora-19-x86_64-DVD/Fedora-19-x86_64-CHECKSUM (1.14 kB)
Fedora-19-x86_64-DVD/Fedora-19-x86_64-DVD.iso (4.49 GB)
```

## RPM: THE RPM PACKAGE MANAGER

RPM (RPM Package Manager; www.rpm.org) works only with software packages built for processing by RPM; it can download, install, uninstall, upgrade, query, and verify RPM packages. The files that hold these packages have a filename extension of **.rpm**. RPM uses the local RPM installation database to track the locations where software packages are installed, the versions of the installed packages, and the dependencies between the packages. RPM uses the Berkeley Database (Berkeley DB or BDB) and stores the database files in **/var/lib/rpm**. RPM forms the basis for **yum**/**yum** finds packages, downloads them from repositories, and then calls RPM to install/upgrade/remove the packages.

Source RPM packages are frequently found in a directory named **SRPMS** (source RPMs), whereas binary RPM packages usually reside in **Packages**. When you download binary packages, make sure they are relevant to the local operating system (both distribution and release—for example, Fedora 15). They should also be compiled for the appropriate processor architecture:

- **i386** covers all Intel- and most AMD-based systems; the N and Z Series Atom processors are also based on this architecture.
- **i586** covers Pentium-class or higher processors.
- `i686` refers to Pentium II or better and includes MMX extensions.
- `S390x` is for IBM System/390.
- `ia64` is for the Intel 64-bit Itanium (not compatible with `x86_64`)
- `alpha` is for the DEC/Compaq Alpha chip.
- `ppc` and `ppc64` denotes the Power PC 32- and 64-bit processors.
- `x86_64` is for Intel and AMD 64-bit processors (not Itanium); the 230 and 330 Series Atom processors are also based on this architecture.
- `sparc` covers the Sun Sparc processor.
- **noarch** The name of the `rpm` file contains almost all the necessary information. Packages marked **noarch** ("no architecture") contain resources, such as images or scripts, that are run by an interpreter. You can install and run **noarch** packages on any architecture.

> 1. Many RPM packages run on releases and even distributions other than the ones they were compiled for. However, installing packages intended for other distributions can create problems.

**yumdownloader** See page 540 for instructions on using **yumdownloader** to download RPM package files.

### QUERYING PACKAGES AND FILES

The following `rpm` command displays a list of one-line summaries of all packages installed on the system:

```bash
$ rpm -qa
samba-common-4.0.9-1.fc19.x86_64
mythes-1.2.3-4.fc19.x86_64
gnome-themes-standard-3.8.4-2.fc19.x86_64
xorg-x11-drv-openchrome-0.3.1-1.fc19.x86_64
caribou-0.4.11-1.fc19.x86_64
gnome-shell-3.8.4-2.fc19.x86_64
gst-plugins-good-0.10.31-9.fc19.x86_64
libm1-1.1-17.fc19.x86_64
gnome-shell-extension-window-list-3.8.4-1.fc19.noarch
...
```

The **-q** option queries the package database; the **-a** option specifies all packages. Without **-a**, **-q** takes the name of a package as an argument and displays information about that package only. For instance, `rpm -q ypserv` tells you whether the **ypserv** package is installed and, if so, which version is installed. Use the **-ql** options to list the files in a package.

```bash
$ rpm -q ypserv
package ypserv is not installed
```

```bash
$ rpm -ql logrotate
/etc/cron.daily/logrotate
/etc/logrotate.conf
/etc/logrotate.d
/usr/sbin/logrotate
/usr/share/doc/logrotate-3.8.4
/usr/share/doc/logrotate-3.8.4/CHANGES
/usr/share/doc/logrotate-3.8.4/COPYING
/usr/share/man/man5/logrotate.conf.5.gz
/usr/share/man/man8/logrotate.8.gz
/var/lib/logrotate.status
```
