
cd snort-<version>
./configure

It is at the point of running the configure script where many compile-time options can be set. To obtain a list of some of these options, notably options to enable support for certain databases or enable certain other features, type the following:

./configure -help

In addition, the INSTALL document and other documentation within the <snort-source>/doc directory explain these and other options available when compiling Snort from source.

Running the configure script, along with any options, will result in Snort looking for various prerequisites. For example, when compiling Snort from source, you might receive an error indicating that one or more prerequisites can't be found, such as this error:

checking for pcre.h... no
ERROR! Libpcre header not found, go get it from
http://www.pcre.org

With that error in mind, I was able to install the pcre development files, rerun the configure script, and continue.

After the configure script has run successfully, compile the software by typing this:

make

The software will now compile. Should you get any errors during this phase, consult the Snort documentation and mailing list archives to see whether you've received a known error for your architecture.

Finally, after the software is compiled, install it by typing the following:

make install

The software will now be installed and should be ready to use. By default, the software is installed into /usr/local/bin. You can test the basic Snort command by typing this:

/usr/local/bin/snort -?

You should see output with help options, similar to this:

     ,,,      -*> Snort! <*- 
 o' )~   Version 2.3.3 (Build 14)
 `;~`    By Martin Roesch & The Snort Team: http://www.snort.org/team.html
        (C) Copyright 1998-2004 Sourcefire Inc., et al.

USAGE: ./snort [-options] <filter options>
Options:
  -A      Set alert mode: fast, full, console, or none (alert file alerts only)
          "unsock" enables UNIX socket logging (experimental).
  ...

## 11.4.2 Configuring Snort

The source code for Snort includes a sample configuration file. If you’ve installed from your distribution’s package, that too should include a sample Snort configuration file. Usually this file is called snort.conf. On most popular distributions, including SUSE and Debian, this file (along with a number of Snort rules) is placed in /etc/snort.

If you’re working with a source installation, the sample snort.conf configuration file is located in <snort-source>/etc/ and sample rules are located in <snort-source>/rules/. For those working with a source-code version, I recommend creating a directory in either /etc/ or /usr/local/etc/ called snort and placing the snort.conf configuration file and the Snort rules in that directory. In addition, the default Snort configuration file calls various map and extra configuration files as well. These files can also be found in the <snort-source>/etc/ directory. Creating the directory and copying all the files into it would look like this (again, this is applicable only to those who have compiled Snort from source):

mkdir /etc/snort
cp <snort-source>/etc/snort.conf /etc/snort/
cp <snort-source>/etc/*.map /etc/snort/
cp <snort-source>/etc/*.config /etc/snort/
cp <snort-source>/rules/* /etc/snort/

One additional and important change is done to the snort.conf configuration file. After you’ve copied it to the /etc/snort directory, edit the file and change the RULE_PATH variable from its default of ../rules to /etc/snort. The line should look like this when you’re done:

var RULE_PATH /etc/snort

Finally, create the Snort log directory with the following command:

mkdir /var/log/snort

With all the groundwork done, it’s time to officially start Snort for the first time. If you’ve installed from your distribution’s package, it’s likely that you can start Snort through the normal run control mechanism, such as /etc/init.d/snort start. If you’ve compiled from source, you’ll need to start Snort manually and point to the location of its configuration file:

/usr/local/bin/snort -c /etc/snort/snort.conf

If you receive any errors, chances are that there are missing files. Check the Snort source directory structure for the missing files and copy them to the appropriate location, based on the configuration file.

If all goes well, you should see a message such as this, near the end of the output:

=== Initialization Complete ===

As you can see, the shell prompt didn’t return. This is because Snort was not told to fork into daemon mode. Press Ctrl+C to kill Snort and add -D to the command line. It should now look like this:

/usr/local/bin/snort -c /etc/snort/snort.conf -D

Snort will start again and this time fork off into the background, returning you to the shell prompt.

There is, of course, much more to Snort configuration than merely getting it running with the default options and rulesets. For more information on specific Snort configurations, refer to the Snort documentation.

### 11.4.3 Testing Snort

With Snort now running in the background, you could assume that it’s running perfectly fine and that log entries will be placed into `/var/log/snort` for you. However, I’m not one to assume things, especially about computer security. Therefore, to test the Snort installation I’ll use the handy hping2 tool to craft a packet or two and fire them toward the host running Snort.

In this case, I’m just looking for verification that Snort is running and monitoring something. The default rules look for bad packets, so crafting one of those should be trivial with hping2. From another host on the network (192.168.1.10), I ran the following hping2 command toward the host running Snort (192.168.1.2):

hping2 -X 192.168.1.2

The `-X` option causes an Xmas scan to be run. Looking in `/var/log/snort` on the host running Snort reveals the alert file has received some information and there is also a new directory called 192.168.1.10, which was the source of the test packets. Inside that directory are files corresponding to the packets I sent, the contents of which are shown here:

[**] BAD-TRAFFIC tcp port 0 traffic [**]
06/07-16:19:00.712543 192.168.1.10:1984 -> 192.168.1.2:0
TCP TTL:64 TOS:0x0 ID:48557 Iplen:20 DgmLen:40
*2***** Seq: 0xED1609B Ack: 0x13E89C5 Win: 0x200 TcpLen: 20
=================================================================
[**] BAD-TRAFFIC tcp port 0 traffic [**]
06/07-16:19:00.712610 192.168.1.2:0 -> 192.168.1.10:1984
TCP TTL:64 TOS:0x0 ID:10034 Iplen:20 DgmLen:40 DF
***A*R** Seq: 0x0 Ack: 0xED1609B Win: 0x0 TcpLen: 20
=================================================================

As you can see from the output, Snort has captured what it believes to be (correctly so) bad TCP packets. The alert log file `/var/log/snort/alert` also contains information that is especially useful for sorting the alerts. Here are the log entries from the alert log file that correspond to the previously shown entries from the specific host file:

[**] [1:524:8] BAD-TRAFFIC tcp port 0 traffic [**]
[Classification: Misc activity] [Priority: 3]
06/07-16:19:00.712543 192.168.1.10:1984 -> 192.168.1.2:0
TCP TTL:64 TOS:0x0 ID:48557 Iplen:20 DgmLen:40
*2***** Seq: 0xED1609B Ack: 0x13E89C5 Win: 0x200 TcpLen: 20

[**] [1:524:8] BAD-TRAFFIC tcp port 0 traffic [**]
[Classification: Misc activity] [Priority: 3]
06/07-16:19:00.712610 192.168.1.2:0 -> 192.168.1.10:1984
TCP TTL:64 TOS:0x0 ID:10034 Iplen:20 DgmLen:40 DF
***A*R** Seq: 0x0 Ack: 0xED1609B Win: 0x0 TcpLen: 20

As you can see from these entries, there are some additional items such as *Classification* and *Priority* that can help to, well, classify and prioritize the alert. Both the classification and the priority can be configured within the alert log file.

### 11.4.4 Receiving Alerts

I recommend working with Snort to gain experience with rules and configuration options before configuring it to send alerts in email or via another means. You might easily find yourself overwhelmed by alerts with the default Snort rules, depending on your network layout.

Recall from Chapter 10 that log file monitoring software was introduced and a recipe was given for using Swatch to monitor log files for certain events, at which time it would send an email based on the alert. If you see where I’m going with this, then congratulations!

#### USING SWATCH TO MONITOR FOR SNORT ALERTS

With its default configuration, Snort logs to `/var/log/snort/alert`. Therefore, creating a Swatch configuration to monitor this file is quite easy. Again, it would be easy to overwhelm yourself or the system with alerts and emails from Swatch, so you should use caution when configuring any actions based on Snort alerts until you’ve had a chance to configure Snort further.

Recall that Snort logs some prioritization data within `/var/log/snort/alert`. Therefore, you could set up a Swatch rule to watch for anything with a certain priority, say 3, for example, and send an email when that’s seen. This would be placed within your Swatch configuration file which, by default, is `~/.swatchrc`. Here’s the configuration entry:

watchfor /Priority: 3/
mail

Starting Swatch and pointing it toward the Snort alert file, `/var/log/snort/alert`, looks like this:

swatch --tail-file=/var/log/snort/alert

Now when an alert with Priority: 3 is logged, an email will be sent by Swatch.

### 11.4.5 Final Thoughts on Snort

Snort comes highly recommended as a means to automate the task of intrusion detection. I’ve only been able to touch on the very basics of Snort here in hopes of giving you a starting point
