
# Snort Configuration

file is called **snort.conf**. On most popular distributions, including SUSE and Debian, this file (along with a number of Snort rules) is placed in `/etc/snort/`.

If you're working with a source installation, the sample `snort.conf` configuration file is located in `<snort-source>/etc/` and sample rules are located in `<snort-source>/rules/`. For those working with a source-code version, I recommend creating a directory in either `/etc/` or `/usr/local/etc/` called `snort` and placing the `snort.conf` configuration file and the Snort rules in that directory. In addition, the default Snort configuration file calls various map and extra configuration files as well. These files can also be found in `<snort-source>/etc/` directory. Creating the directory and copying all the files into it would look like this (again, this is applicable only to those who have compiled Snort from source):

```bash
mkdir /etc/snort
cp <snort-source>/etc/snort.conf /etc/snort/
cp <snort-source>/etc/*.map /etc/snort/
cp <snort-source>/etc/*.conf /etc/snort/
cp <snort-source>/rules/*.rules /etc/snort/
```

One additional and important change is done to the `snort.conf` configuration file. After you've copied it to `/etc/snort` directory, edit the file and change the `RULE_PATH` variable from its default of `../rules` to `/etc/snort`. The line should look like this when you're done:

```bash
var RULE_PATH /etc/snort
```

Finally, create the Snort log directory with the following command:

```bash
mkdir /var/log/snort
```

With all the groundwork done, it's time to officially start Snort for the first time. If you've installed it from your distribution's package, it is likely that you can start Snort through the normal run control mechanism, such as `/etc/init.d/snort` start. If you've compiled from source, you'll need to start Snort manually and point to the location of its configuration file:

```bash
/usr/local/bin/snort -c /etc/snort/snort.conf
```

If you receive any errors, chances are that there are missing files. Check the Snort source directory structure for the missing files and copy them to the appropriate location, based on the configuration file.

If all goes well, you should see a message such as this, near the end of the output:

```text
=== Initialization Complete ===
```

As you can see, the shell prompt didn't return. This is because Snort was not told to fork into daemon mode. Press Ctrl+C to kill Snort and add a `-D` to the command line. It should now look like this:

```bash
/usr/local/bin/snort -c /etc/snort/snort.conf -D
```

Snort will start again and this time fork off into the background, returning you to the shell prompt.

There is, of course, much more to Snort configuration than merely getting it running with the default options and rulesets. For more information on specific Snort configurations, refer to the Snort documentation.

## Testing Snort

With Snort now running in the background, you could assume that it’s running perfectly fine and that log entries will be placed into /var/log/snort for you. However, I’m not one to assume things, especially about computer security. Therefore, to test the Snort installation I’ll use the handy hping2 tool to craft a packet or two and fire them toward the host running Snort.

In this case, I’m just looking for verification that Snort is running and monitoring something. The default rules look for bad packets, so crafting one of those should be trivial with hping2. From another host on the network (192.168.1.10), I ran the following hping2 command toward the host running Snort (192.168.1.2):

```bash
hping2 -X 192.168.1.2
```

The `-x` option causes an Xmas scan to be run. Looking in /var/log/snort on the host running Snort reveals that the alert file has received some information and there is also a new directory called 192.168.1.10, which was the source of the test packets. Inside that directory are files corresponding to the packets I sent, the contents of which are shown here:

```text
[**] BAD-TRAFFIC tcp port 0 traffic [**]
06/07-16:19:00.712543 192.168.1.10:1984 -> 192.168.1.2:0
TCP TTL:64 TOS:0x0 ID:48557 IpLen:20 DgLen:40
*2****** Seq: 0xED1609B Ack: 0x13E893C5 Win: 0x200 Tcplen: 20
+++=+-=-++===-++===-+++---++++=---====-++====-++++==
```

```text
[**] BAD-TRAFFIC tcp port 0 traffic [**]
06/07-16:19:00.712610 192.168.1.2:0 -> 192.168.1.10:1984
TCP TTL:64 TOS:0x0 ID:10034 IpLen:20 DgLen:40 DF
***AR*** Seq: 0x0 Ack: 0xED1609B Win: 0x0 Tcplen: 20
****=-***++==*+==-*=**+==***+==***-****=***==***==
```

As you can see from the output, Snort has captured what it believes to be (correctly so) bad TCP packets. The alert log file /var/log/snort/alert also contains information that is especially useful for sorting the alerts. Here are the log entries from the alert log file that correspond to the previously shown entries from the specific host file:

```text
[**] [1:524:8] BAD-TRAFFIC tcp port 0 trafffic [**]
[Classification: Misc activity] [Priority: 3]
06/07-16:19:00.712543 192.168.1.10:1984 --> 192.168.1.2:0
TCP TTL:64 TOS:0x0 ID:48557 IpLen:20 DgLen:40 DF
*2****** Seq: 0xED1609B Ack: 0x13E893C5 Win: 0x200 Tcplen: 20
```

```text
[**] [1:524:8] BAD-TRAFFIC tcp port 0 trafffic [**]
[Classification: Misc activity] [Priority: 3]
06/07-16:19:00.712610 192.168.1.2:0 --> 192.168.1.10:1984
TCP TTL:64 TOS:0x0 ID:10034 IpLen:20 DgLen:40 DF
****A**** Seq: 0x0 Ack: 0xED1609B Win: 0x0 Tcplen: 20
```

As you can see from these entries, there are some additional items such as **Classification** and **Priority** that can help to, well, classify and prioritize the alert. Both the classification and the priority can be configured within the alert log file.

## Receiving Alerts

I recommend working with Snort to gain experience with rules and configuration options before configuring it to send alerts in email or via another means. You might easily find yourself overwhelmed by alerts with the default Snort rules, depending on your network layout.

Recall from Chapter 10 that log file monitoring software was introduced and a recipe was given for using Swatch to monitor log files for certain events, at which time it would send an email based on the alert. If you see where I'm going with this, then congratulations!

### USING SWATCH TO MONITOR FOR SNORT ALERTS

With its default configuration, Snort logs to /var/log/snort/alert. Therefore, creating a Swatch configuration to monitor this file is quite easy. Again, it would be easy to overwhelm yourself or the system with alerts and emails from Swatch, so you should use caution when configuring any actions based on Snort alerts until you've had a chance to configure Snort further.

Recall that Snort logs some prioritization data within /var/log/snort/alert. Therefore, you could set up a Swatch rule to watch for anything with a certain priority, say 3, for example, and send an email when that's seen. This would be placed within your Swatch configuration file which, by default, is ~/.swatchsrc. Here's the configuration entry:

```text
watchfor /Priority: 3/
mail
```

Starting Swatch and pointing it toward the Snort alert file, /var/log/snort/alert, looks like this:

```text
swatch --tail-file=/var/log/snort/alert
```

Now when an alert with **Priority: 3** is logged, an email will be sent by Swatch.

# Final Thoughts on Snort

Snort comes highly recommended as a means to automate the task of intrusion detection. I’ve only been able to touch on the very basics of Snort here in hopes of giving you a starting point for working with it. From here, you can combine Snort with MySQL and ACID to create an enterprise-class intrusion detection system. Snort can be configured just as you need and extended to fit any size of organization.

# Monitoring with ARPWatch

ARPWatch is a daemon that watches for new Ethernet interfaces on a network. If a new ARP entry is seen, it could be indicative of a rogue computer somewhere within the network.

ARPWatch uses the PCap library, which may not (yet) be on your system. If it’s not, you’ll find out during the configuration process for ARPWatch. The PCap library, commonly known as libpcap, can be downloaded from http://www.tcpdump.org/. The PCap library is used for other network and security-related programs such as TCPDump. Because TCPDump was already covered, I’ll forgo repeating the instructions for installing libpcap in this chapter and instead I’ll refer you to the section “TCPDump: A Simple Overview” for those instructions.

Installation of ARPWatch involves unwrapping the ARPWatch archive that you download, usually something like `tar -zxvf arpwatch.tar.Z`. From there, change directory into the ARPWatch directory and run the configure script.

```bash
./configure
```

You’ll see a (hopefully somewhat) familiar series of output statements, something like this:

```text
creating cache ./config.cache
checking host system type... i686-pc-linux-gnu
checking target system type... i686-pc-linux-gnu
checking build system type... i686-pc-linux-gnu
checking for gcc... gcc
checking whether the C compiler (gcc ) works... yes
... (output truncated) ...
```

If you see an error to the effect of the following, you’ll need to install libpcap:

```text
checking for main in -lpcap... no
configure: error: see the INSTALL doc for more info
```

Refer to the section on TCPDump earlier in this chapter for information on installing the PCap library.
