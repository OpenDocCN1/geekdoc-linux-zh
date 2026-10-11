uses signatures to analyze the network traffic. Once a given packet matches a signature, Snort can generate an alert. Signatures not only exist for many computer viruses and spyware, but also for network traffic, such as BitTorrent, ICQ, Skype or even Hotmail access. They are available from SourceForge, Inc., through the Snort Web site, and through Bleeding Edge Threats (see Resources). PacketFence also ships with an OinkMaster configuration to obtain and cut down the ruleset automatically to only what is required by PacketFence. Because PacketFence support for Snort 2.6 is still under development, download Snort 2.4.5 from www.snort.org/lib/linux/old, and then install the RPM by executing:

```
```bash
rpm -ivh snort-2.6.5-1.RHEL4.1386.rpm
```
```

Nessus, on the other hand, is an active vulnerability scanner—meaning that it generates connections to the hosts you want to test for vulnerabilities. You have to register with Tenable Network Security, the owner of Nessus, in order to receive the available plugins. Install Nessus by downloading version 2.2.9 for Linux and executing:

```
```bash
sh nessus-installer-2.2.9.sh
```
```

Nessus 3 is not yet well supported, and due to the licensing issues surrounding it, stick with 2.2.9.
Once the installation finishes, start Nessus with:

```
```bash
/opt/nessus/sbin/nessusd -D
```
```

and test the connection with NessusClient, which is available as a separate download.

# Installation

Download the PacketFence RPM from the SourceForge repository, and install it using:

```
```bash
rpm -ivh packetfence-1.8.2-0.1386.rpm
```
```

In /usr/local/pf, you will find two Perl scripts that will help you with the necessary configuration steps: installer.pl and configurator.pl. Change your current directory to /usr/local/pf, and execute installer.pl. The script, among other things, sets up the PacketFence database, installs all the necessary Perl modules (which are quite a few) and creates a user account for the Web GUI.

# Configuration Steps

Now, the real configuration work starts. First, execute configurator.pl, and you’ll be offered several choices. Choose the template configuration based on the testing mode. You’ll be asked to supply several network parameters (DHCP servers, DNS servers and so on), and a basic configuration file, /usr/local/pf/conf/pf.conf, will be created. This configuration file contains only the differences you apply to the default configuration parameters saved in /usr/local/pf/conf/pf.conf.defaults. Have a look at conf/pf.conf.defaults to get an idea of the available options. To help you see what’s going on inside PacketFence, add the following lines to

# Expert Included.

![](bbox=[0.41, 0.51, 0.96, 0.92])

Shane’s customers are always pushing the limits of technology. That’s why he is a fan of the Rackform iSvr R2020, an innovative, iU, two-compute-node system designed to increase computing density while reducing cost, energy, and space requirements. With support for two Quad-Core Intel® Xeon® Processors 5300 Series per compute node, the iSvr R2020 combines Intel’s proven reliability with industry-leading 16-core-per-iU density. Additionally, 8 Fully Buffered DIMM sockets, 2 hot-swap SATA hard drives, and a PCI-Express slot in each compute node convince Shane that the iSvr R2020 provides the density, flexibility, and cost effectiveness needed to tackle even the most demanding computing challenges.

When you partner with Silicon Mechanics, you get more than a powerful Intel Solution — you get an expert like Shane.

![](bbox=[0.04, 0.79, 0.44, 0.88])

visit us at www.siliconmechanics.com
or call us toll-free at 866-352-1173

![](bbox=[0.84, 0.53, 0.96, 0.65])

![](bbox=[0.04, 0.79, 0.44, 0.88])