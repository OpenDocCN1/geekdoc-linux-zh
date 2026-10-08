
You have to have an Ethernet adapter to be connected to an Ethernet network. Make sure that your Ethernet adapter is plugged in to your computer’s motherboard — snugly. Sometimes, you have to pull out the adapter and then reinsert it. The process of pulling out an adapter and then plugging it back in is called reseating.

## Is your network adapter configured correctly?

Sometimes a startup script is misconfigured, which causes the startup screen to go by without your seeing an error message. If that happens, log in as root and from the shell prompt and type this command:

```
ifconfig
```

You see a listing of two different interfaces, as shown in the following code, or three interfaces if you have PPP configured. The `ifconfig` command tells the Linux kernel that you have a network adapter and gives it an IP address and network mask. This step is the first in connecting your Linux computer to your network:

```
eth0 Link encap:10Mbps Ethernet HWaddr 00:A0:24:2F:30:69
inet addr:192.168.1.1 Bcast:192.168.1.255 Mask:255.255.255.0
UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
RX packets:16010 errors:18 dropped:18 overruns:23 TX packets:7075 errors:0 dropped:0 overruns:0
Interrupt:10 Base address:0x300

lo Link encap:Local Loopback
inet addr:127.0.0.1 Bcast:127.255.255.255 Mask:255.0.0.0
UP BROADCAST LOOPBACK RUNNING MTU:3584 Metric:1
RX packets:115 errors:0 dropped:0 overruns:0
TX packets:115 errors:0 dropped:0 overruns:0
```

## Checking your wireless NIC

Linux provides several tools to work with Wi-Fi network interfaces. Red Hat installs the wireless-tools RPM package by default. The tools include `ifconfig`, `iwspy`, and other utilities. We describe how to use `iwconfig` to examine your Wi-Fi interface configuration.

### "I is an engagere"

An experienced electrical engineer and Linux author once got really angry with a cable TV company. His cable service went dead in the middle of a Philadelphia Eagles game. It didn't matter that the Eagles were losing — he wanted to see the game because the Eagles don't appear on TV often in Albuquerque. The engineer called the cable company immediately. Blah! Blah! Blah! My connection — Blah!

Blah! The nice support person guided the poor engineer step-by-step through his own fault tree. Step 1: Is your VCR or TV turned on? "Yes, of course." Step 2: Is the VCR button on your VCR toggled on? "Of course — ah, whoops, no, it isn't. Ah, yes, it works now, thank you very much. Goodbye." D'oh! What was five years of electrical engineering school good for?

Log in as root, open a GNOME Terminal window (refer to Chapter 4 for more information), and run the iwconfig command. If your NIC is configured correctly, you see output similar to this example:

```
lo            no wireless extensions.

eth0      IEEE 802.11-DS  ESSID:"linky"  Nickname:"..."
          Mode:Ad-Hoc  Frequency:2.437GHz  Cell: "..."
          Bit Rate:11Mb/s   Tx-Power=15 dBm  Sensitivity:1/3
          Retry limit:4     RTS thr:off   Fragment thr:off
          Encryption key:A654-6277-43D6-ACC3-6E6D-1C12-98
          Power Management:off
          Link Quality:0  Signal level:0  Noise level:0
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid ...
          Tx excessive retries:0  Invalid misc:0  Missed ...
```

These options are the important ones to examine:

- **Mode:** You have to set this value to Ad-Hoc when you're connecting to an ad hoc network. (Refer to Chapter 7 for more information about this method.) You can use the value Any when you're connecting to an infrastructure network. The Any value can work for an ad hoc network in some cases; however, a description of those cases is beyond the scope of this book, so use ad-hoc mode whenever necessary.
- **ESSID:** You have to use the same value on every machine connected to an ad hoc LAN. For example, every machine on the network is given the ESSID linky.
- **Encryption key:** You have to use the same encryption key on every machine connected to your wireless network. The key comes in two flavors: 40 bit and 128 bit. The 40-bit key is nearly useless because it can be readily cracked by hackers using widely available software.

Your wireless network should work as long as you set these parameters correctly and your computer is within range of the other devices on your LAN. The other parameters are either self generating or unimportant in getting the card to work.

## Maybe the physical connections aren't set up right

If you don't see the line containing `lo`, which is the loopback interface, or `eth0`, which is your network adapter, your physical network connections aren't set up right. The loopback interface isn't a physical device; it's used for the network software's internal workings. The loopback interface must be present for the network adapter to be configured.

If the loopback interface isn't present, type this command:

```
ifconfig lo 127.0.0.1
```

If the network adapter — generally an Ethernet card — isn't present, type this command:

```
ifconfig eth0 192.168.1.1
```

Because this address is a class C network address, `ifconfig` automatically defaults to the `255.255.255.0` netmask. If you have an unusual netmask, which you shouldn't, type this command:

```
ifconfig eth0 192.168.1.1 netmask 255.255.255.0
```

Type `ifconfig` and your network adapter should be displayed correctly. If it's not, examine the manual page on `ifconfig`. You display this manual page by typing this command and then pressing Enter:

```
man ifconfig
```

You can page through the document in several ways: Press Enter to go line by line, press the spacebar to go forward one page at a time, press Ctrl+B to page backward, or press Q to quit. The `ifconfig` man page shows a great deal of information about what `ifconfig` is and how it works. If you're still having problems, look at the Linux startup information by running this command:

```
dmesg | more
```

Note that you pipe (use the `|` symbol) the output from `dmesg` to the `more` command. Linux pipes are used to transmit the output command to the input of another. After you run the preceding command, you see the information that was displayed during the boot process. The `more` command shows one page of information at a time; press the spacebar to display each subsequent page.

![](img/8c094d1b36276212c03d10d898508a6e_291_0.png)

## Maybe you have a hardware problem

If you don't see your Ethernet adapter, you may have a hardware problem. Check your adapter. **Reset it** (take it out and put it back in) and see whether it works. If not, you probably need a new NIC. If you do see the NIC, look inside the Linux kernel and see which devices it has. Type this command to change to a special directory named /proc, where process information is located:

```
cat /proc/devices
```

You should see a line with your network adapter listed. If you don't, Linux doesn't know that it exists.

![](img/8c094d1b36276212c03d10d898508a6e_292_0.png)

Try to run your Ethernet NIC again. If it still doesn't run, you have to find out more information.

## Maybe you have an interrupt or address conflict

You may have an interrupt or address conflict. Look at the list of interrupts and then the I/O addresses of all the devices that the kernel knows about, by typing these commands:

```
cat /proc/interrupts
cat /proc/ioports
```

The I/O address is the location in memory where the device, such as the network adapter, is accessed by the microprocessor (for example, your Pentium chip). The interrupt communicates to the microprocessor that it should stop whatever it's doing in order to process information that has arrived at the device sending the interrupt.

When your Ethernet adapter receives a packet, it sends an interrupt to the microprocessor to signal that an event has occurred. Your Pentium stops what it's doing and processes the new information. The microprocessor even interacts with Linux to do the processing.

Type **cat /proc/interrupts** to show both the interrupts and the I/O addresses with which Red Hat Linux is familiar. The output should look like this example:

```
0: 378425 timer
1: 1120 keyboard
2: 0 cascade
10: 16077 3c509
13: 1 math error
14: 63652 + ide0
```

This listing shows that Linux knows that the Ethernet NIC (3c509) exists. That's a good sign.
