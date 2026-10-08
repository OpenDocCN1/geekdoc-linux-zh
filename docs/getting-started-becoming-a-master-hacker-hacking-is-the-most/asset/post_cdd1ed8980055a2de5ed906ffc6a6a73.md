
## 10

**Sniffers for Network and Protocol Analysis**

A series of persistent, small wins will defeat any opponent.

Master OTW

A network sniffer—sometimes referred to as a packet analyzer, protocol analyzer, or network traffic analyzer—can intercept and analyze network traffic that traverses a digital network. These sniffers can be invaluable to the network or security engineer, the forensic investigator—and in some cases—the hacker. For instance, if an application sends passwords over the network unencrypted, the hacker may be able to sniff and view the passwords.

Since only a few applications send passwords unencrypted in our security-conscious era, the value of the sniffer to the hacker is a bit more nuanced.

For some exploits/hacks, such as DNS or MiTM attacks, analysis of the LAN traffic can be crucial to their success, making the sniffer invaluable. Besides, sniffing a target’s traffic can reveal what sites they are visiting, their cookies, their user agent, or even their email messages (if unencrypted or you have the resources to decrypt the message).

Many tools are capable of network sniffing, including:
- SolarWinds Deep Packet Inspection and Analysis Tool
- Tcpdump
- Windump
- Wireshark
- Network Miner
- Capsa
- tshark

In this chapter, we use two of the most popular network sniffer/analyzer: **tcpdump** and **Wireshark**. In addition, we use Wireshark to dig deep into the NSA’s EternalBlue exploit to understand exactly how it works.

**Controversial Use of Sniffers**

For over twenty years, the Federal Bureau of Investigation (FBI) in the United States has used a tool they term “Carnivore.” This tool is used to sniff and analyze the traffic of people suspected of committing crimes. It is very controversial, but legal, as it allows the FBI to eavesdrop on network traffic without a warrant.

**Prerequisites to Sniffing**

It’s critical to point out that to effectively use a network sniffer, your network interface card (NIC) should be in promiscuous mode. This means that your NIC picks up ANY packet traversing the network.

Usually, NICs only pick up packets that are intended for its particular MAC (globally unique physical) address.

The other critical point to understand with network sniffing is that the standard file format for sniffing is .pcap (packet capture). This means your system must have a library (a bit of reusable code) to put the packets into this format. These libraries are libpcap on your Linux system or Winpcap on your Windows system.

**tcpdump in Action**

Before we examine the powerful GUI-based sniffer Wireshark, let’s take a brief look at the command line sniffer, tcpdump. Tcpdump was among the very first (1988) Linux/UNIX-based sniffers. Although it may not be the easiest sniffer to use, its versatility and lightweight design make it worth knowing. Tcpdump can be particularly useful if you have to analyze a non-GUI based system or a remote system where a GUI would be slow, inefficient, and not very stealthy.

To start tcpdump, enter:

```text
root@kali-2019:~# tcpdump
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on eth0, link-type EN10MB (Ethernet), capture size 262144 bytes
16:07:04.062010 IP 192.168.0.235.57656 > 239.255.255.250.1900: UDP, length 174
16:07:04.064714 ARP, Request who-has (gateway) tell kali-2019.1299 (length 28)
16:07:04.06517 ARP, Reply gateway is-at b0:be:76:08:b5:3c (oui Unknown), length 46
16:07:04.066326 IP kali-2019.35533 > gateway.domain: 15131+ PTR? 250.255.255.239.in-addr.arpa. (46)
16:07:04.080311 IP gateway.domain > kali-2019.35533: 15132 NXdomain 0/1/0 (103)
16:07:04.080872 IP kali-2019.59304 > gateway.domain: 50202+ PTR? 233.0.168.192.in-addr.arpa. (44)
16:07:04.095554 IP gateway.domain > kali-2019.59304: 50202 NXdomain 0/0/0 (44)
16:07:04.096001 IP kali-2019.43942 > gateway.domain: 28517+ PTR? 1.0.168.192.in-addr.arpa. (42)
16:07:04.111351 IP gateway.domain > kali-2019.43942: 28517 NXdomain 0/0/0 (42)
16:07:04.111687 IP kali-2019.42176 > gateway.domain: 23623+ PTR? 173.0.168.192.in-addr.arpa. (44)
16:07:04.126380 IP gateway.domain > kali-2019.42176: 23623 NXdomain 0/0/0 (44)
16:07:05.006342 IP 192.168.0.235.57656 > 239.255.255.250.1900: UDP, length 174
16:07:07.507418 IP kali-2019.59304 > 224.0.0.251.5390: PTR? (QM) 192.168.0.152.in-addr.arpa. (44)
16:07:07.585756 IP kali-2019.44754 > gateway.domain: 30429+ PTR? 251.0.0.224.in-addr.arpa. (42)
16:07:07.587774 IP gateway.domain > kali-2019.44754: 30433 PTR? 224.0.0.251.192.168.0.152.in-addr.arpa. (81)
16:07:07.601171 IP gateway.domain > kali-2019.44754: 30429 NXdomain 0/1/0 (99)
```

kali > tcpdump

As you can see, as soon as you enter the command tcpdump, packets begin to flow across your screen.

These packets are largely communication between your Kali system and the LAN gateway.

Let's try creating some traffic to analyze. For instance, let's try sending a ping (ICMP echo request) to your Windows 7 system from one terminal and run tcpdump from the other.

kali > ping 192.168.0.114

kali > tcpdump

Let’s zoom in on the tcpdump screen so we can see detail there.

```text
root@kali-2019:~# tcpdump
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on eth0, link-type EN10MB (Ethernet), capture size 262144 bytes
16:12:05.770020 IP kali-2019 > 192.168.0.114: ICMP echo request, id 25881, seq 3, length 64
16:12:05.770314 IP 192.168.0.114 > kali-2019: ICMP echo reply, id 25881, seq 3, length 64
16:12:05.770836 IP kali-2019.44328 > _gateway.domain: 39663+ PTR? 114.0.168.192.in-addr.arpa. (44)
16:12:05.780317 IP _gateway.domain > kali-2019.44328: 39663 NXDOMAIN 0/0/0 (44)
16:12:05.798799 IP kali-2019.37659 > _gateway.domain: 53089+ PTR? 173.0.168.192.in-addr.arpa. (44)
16:12:05.804341 IP _gateway.domain > kali-2019.37659: 53089 NXDOMAIN 0/0/0 (44)
16:12:05.804701 IP kali-2019.39714 > _gateway.domain: 47919+ PTR? 1.0.168.192.in-addr.arpa. (44)
```

```text
root@kali-2019:~# tcpdump host 192.168.0.114
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on eth0, link-type EN10MB (Ethernet), capture size 262144 bytes
09:47:40.607043 IP kali-2019 > 192.168.0.114: ICMP echo request, id 28115, seq 7, length 64
09:47:40.607894 IP 192.168.0.114 > kali-2019: ICMP echo reply, id 28115, seq 7, length 64
09:47:41.608042 IP kali-2019 > 192.168.0.114: ICMP echo request, id 28115, seq 8, length 64
09:47:41.608845 IP 192.168.0.114 > kali-2019: ICMP echo reply, id 28115, seq 8, length 64
09:47:42.608065 IP kali-2019 > 192.168.0.114: ICMP echo request, id 28115, seq 9, length 64
09:47:42.609532 IP 192.168.0.114 > kali-2019: ICMP echo reply, id 28115, seq 9, length 64
09:47:43.609607 IP kali-2019 > 192.168.0.114: ICMP echo request, id 28115, seq 10, length 64
09:47:43.610432 IP 192.168.0.114 > kali-2019: ICMP echo reply, id 28115, seq 10, length 64
09:47:44.611175 IP kali-2019 > 192.168.0.114: ICMP echo request, id 28115, seq 11, length 64
09:47:44.611988 IP 192.168.0.114 > kali-2019: ICMP echo reply, id 28115, seq 11, length 64
09:47:45.612675 IP kali-2019 > 192.168.0.114: ICMP echo request, id 28115, seq 12, length 64
09:47:45.613553 IP 192.168.0.114 > kali-2019: ICMP echo reply, id 28115, seq 12, length 64
09:47:46.616533 IP kali-2019 > 192.168.0.114: ICMP echo request, id 28115, seq 13, length 64
09:47:46.617399 IP 192.168.0.114 > kali-2019: ICMP echo reply, id 28115, seq 13, length 64
```

As you can see, tcpdump displays the protocol (ICMP) and the type (echo request and echo reply).

If we want to capture the output to a file that we can analyze at a later time, we can use the -w option followed by the file name, such as:

kali > tcpdump -w myoutput.cap

**Filter by IP Address**

We may want to filter out all the traffic except the traffic coming back from the Windows 7 system.

Tcpdump--developed by researchers at the Lawrence Livermore National Laboratory in Berkeley, CA, running BSD
