
Parts of MRTG are written in Perl, so Perl also must be installed on the system. Version 5.05 or later is recommended. Several graphics libraries also are required for MRTG to function correctly, but their installation is beyond the scope of this chapter. Refer to the doc/unix-guide.txt document (in the MRTG source directory covered shortly) for the exact requirements.

## MRTG Installation

MRTG should be downloaded from http://people.ee.ethz.ch/~oetiker/webtools/mrtg/pub/ and placed in the appropriate directory. For this example, /usr/src is used. The current version of MRTG at the time of publication is 2.9.12, which is used here.

After downloading the MRTG package, follow these steps.

- 1. Log in as root and move into the directory where the package was downloaded:
  `[root@lefty /root]# cd /usr/src`

- 2. Unzip the distribution:
  `[root@lefty src]# gunzip mrtg-2.9.12.tar.gz`

- 4. Untar the tarball:
  `tar xvf mrtg-2.9.12.tar`

- 5. This will create the MRTG source tree. Move into the source tree:
  `[root@lefty src]# cd mrtg-2.9.12`

- 6. Execute the configure script:
  `[root@lefty mrtg-2.9.12]# ./configure`

- 7. Execute the make command:
  `[root@lefty mrtg-2.9.12]# make`

- 8. Finally, execute the make install:
  `[root@lefty mrtg-2.9.12]# make install`

This will create the installation directory structure, /usr/local/mrtg-2/, and move all the binaries and appropriate files into the directory. Move into the directory structure:
`[root@lefty mrtg-2.9.12]# cd /usr/local/mrtg-2/`

MRTG needs a directory that is accessible by the web server. A common directory location for HTML documents for the Apache Web Server on Linux is /home/httpd/html/, so the MRTG files can be placed in a subdirectory:
`[root@lefty mrtg-2]# mkdir /home/httpd/html/mrtg`

Be sure to use an appropriate directory based upon the web server's configuration. A configuration directory for MRTG also should be created:
`[root@lefty mrtg-2]# mkdir cfg`

![](img/5f0cc5444dfa57f5c5cc6a7830396eaa_304_0.png)

Figure 15.3 MRTG web directory.

![](img/5f0cc5444dfa57f5c5cc6a7830396eaa_304_1.png)

Figure 15.4 MRTG interface statistics.

Now the system must be configured to run mrtg on a regular basis. Use crontab with the -e option to make mrtg run every five minutes:

```
[root@lefty mrtg-2]# crontab -e
```

and add the following entry:

```
0,5,10,15,20,25,30,35,40,45,50,55 * * * * /usr/local/mrtg-2/bin/mrtg
/usr/local/mrtg-2/cfg/mrtg.cfg
```

Additional routers and nodes can be added to the mrtg.cfg with the following command:

```
[root@lefty mrtg-2]# bin/cfgmaker --global 'WorkDir: /home/http/html/mrtg' readaccess@192.168.1.254 >>/usr/local/mrtg-2/cfg/mrtg.cfg
```

As mentioned, the data is still in a somewhat raw format. MRTG includes a tool called indexmaker that will create an index page that links to all the nodes being monitored. To create an index for this example, the following command is used:

```
[root@lefty mrtg-2]# bin/indexmaker /usr/local/mrtg-2/cfg/mrtg.cfg
> /home/http/html/mrtg/index.html
```

## Permissions and Ownership Issues With the index.html File

The index.html file's permissions and ownership might need to be manually set to make the file readable by the owner of the web server process.

This creates the index.html with URLs pointing to all the nodes via a graphic summary—as shown in Figure 15.5.

![](img/5f0cc5444dfa57f5c5cc6a7830396eaa_305_0.png)

Figure 15.5 MRTG with index page.

After a new node has been added using cfgmaker, be sure to run the indexmaker again. After mrtg has been configured with the nodes to monitor and given time to collect the statistical information, the index page will resemble Figure 15.6.

![](img/5f0cc5444dfa57f5c5cc6a7830396eaa_306_0.png)

## IPTraf

IPTraf is a network monitoring tool that is geared towards real-time monitoring of network traffic. Unlike a sniffer, such as tcpdump, IPTraf reports the statistics of the traffic as seen by the Linux network driver. Like a sniffer, IPTraf requires the interface to be placed in promiscuous mode; consequently, the program should be run as the root user.

IPTraf installation is very simple and straightforward consisting of unzipping, untarring, and running the setup script, so it will not be covered here.

IPTraf is installed to the /usr/local/bin/ directory, so if /usr/local/bin/ is not in your path, then the complete filename /usr/local/bin/iptraf will need to be executed to start the program.
