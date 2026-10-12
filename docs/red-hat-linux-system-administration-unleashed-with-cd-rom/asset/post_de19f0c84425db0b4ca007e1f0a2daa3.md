
## Note

The tcpdump package is installed in the directory /usr/local/sbin by default. Be sure to have this directory listed in your execution path or explicitly specify the directory on the command line.

The command-line options for the tcpdump program are described in the associated manual page and in Table 16.1.

## TABLE 16.1 Tcpdump Command-Line Options

| Option | Description |
|---|---|
| -c count | Terminates program execution after processing count packets. |
| -d | Dumps any compiled packet filtering code to the stdout file descriptor and terminates program execution. |
| -e | For each packet that is captured and processed, prints its associated link-level header. |
| -f | Does not perform address resolution on foreign Internet addresses. |
| -F file | Uses any expressions listed in file to perform filtering on captured packets. It should be noted that using this option results in any filtering options given on the command line being ignored. |
| -i interface | Captures data packets from a particular network interface device. If this option is not given, tcpdump will attempt to automatically find an active network interface, using the lowest numbered device if multiple active interfaces exist. |
| -l | Forces program output into line buffered mode. This option is useful if you are piping output data into another running program, and want to allow the printed data to be processed line by line. |
| -n | Does not perform any resolution of system host addresses or port numbers into alphanumeric symbolic names. |
| -N | When printing resolved host names, does not print their domain qualification information. |
| -O | Prevents the packet filtering code optimizer from being run. This option would normally never be used unless a bug was suspected in the code optimizer routines. |
| -p | Does not force the network interface device into promiscuous mode upon program execution. It is important to note that using this option will not guarantee that promiscuous mode will be disabled; it simply prevents the mode from being turned on explicitly by the running instance of tcpdump. |

## TABLE 16.1 continued

| Option | Description |
|---|---|
| -q | Outputs less detailed packet decode information per packet. |
| -r file | Processes packet data stored in file, instead of capturing data from a live network interface. If file is specified as "-", the stdin file descriptor is used as the input source. |
| -s length | Captures up to length bytes of data for each packet that is processed. This option allows network sniffing performance to be optimized by preventing the hosts' packet capture routines from retrieving unwanted data. Capturing only the data that is necessary for analysis tasks helps to prevent packet loss when monitoring high-speed networks. If protocol information contained in a captured packet is truncated as a result of this option a [|proto|] indicator is output, where proto is the protocol layer of the packet in which data truncation occurred. If this command-line option is not given, tcpdump defaults to capturing 68 bytes of data per received packet. |
| -S | Prints the true values of transmitted TCP sequence numbers. If this option is not set, tcpdump will attempt to keep track of sequence number state information for TCP virtual circuits, printing sequence number information relative to 0. |
| -t | Disables the output of time stamp information for each captured data packet. |
| -tt | Outputs an unformatted time stamp for each captured data packet. |
| -v | Outputs protocol decode information with a higher level of verbosity. |
| -vv | Outputs protocol decode information with the highest level of verbosity available. |
| -w file | Writes the captured binary packet data to file. The use of this option will prevent the output of decoded protocol information. If file is specified as "-", the binary packet information is output to stdout. |
| -x | Outputs received packet data in hexadecimal format, minus the link-level protocol header. |
| expression | Filters captured packets according to expression. Data packets will only be processed and displayed if expression evaluates as true. Details on how to filter incoming traffic are given in the "Analyzing Types of Traffic" section of this chapter. |

## Uses for Sniffers

Sniffers are extremely valuable tools for detecting network mis-configurations, performing protocol analysis, and monitoring user activity because they are doing application-level protocol analysis. Because they are capable of capturing the actual content of network sessions instead of just the protocol header information, they can provide an extremely in-depth view into network activity.

Denial of service attacks can bring network servers to their knees. Administrators can use sniffers to detect when a denial of service attack is being launched against a host on their network. Quick detection allows attacks to be recovered from faster and more efficiently. The protocol decoding abilities of tcpdump can be used to detect attacks in real-time.

The following is a list of common network denial of service attacks and how to detect them using tcpdump:

- **SYN Flood**—SYN floods are a common type of denial of service attack that involve flooding a target host with invalid connection requests. The target hosts’ connection queue eventually fills, and further connection requests (including legitimate ones) are denied. SYN floods to a particular IP address may be detected using the following tcpdump command:

```
# tcpdump tcp host ip_address
```

Tcpdump will output the decoded tcp protocol information for the host ip_address. Extremely large numbers of TCP SYN packets (specified by the S flag in the output protocol information) can be indicative of SYN flood attacks.

- **Ping of Death**—The Ping of Death is an attack that exploits a flaw in the fragmented packet reconstruction subsystems of many hosts’ TCP/IP network stacks. It involves sending an oversized fragmented packet to a vulnerable host, that when reconstructed, will result in the packet length identifier being overflowed into a negative value. Processing of such packets often results in a crash of the vulnerable machines’ TCP/IP stack. Ping of Death attacks to a particular host can be detected using the following tcpdump command:

```
# tcpdump dst host ip_address
```

Tcpdump will output the decoded protocol information destined for the host ip-address. IP fragments that have a combined offset-length that is greater than 65,535 are indicative of Ping of Death attacks.

- **Smurf**—Smurf involves sending an ICMP ping request to the broadcast address of a network. On networks that are vulnerable to the smurf attack, every active host that receives the ping request will generate a response. This can result in the generation of extremely high network load conditions. Smurf attacks can be detected using the following tcpdump command:

```
# tcpdump icmp dst host broadcast-address
```

Tcpdump will output decoded ICMP protocol information destined for the specified network broadcast address. Any ICMP ping requests are usually indicative of smurf attacks.

Sniffers are also extremely valuable tools for diagnosing network errors and misconfigurations. Many of these problems would be difficult or impossible to detect otherwise because they occur in the low-level network stacks of affected hosts. The tcpdump program allows network dialogs to be examined at the lowest possible level, allowing such problems to be diagnosed easily.

The following is a listing of common network problems and how to detect them using tcpdump:

- **Duplicate Ips**—If it is suspected that two hosts are using the same IP address on a network, such activity can be detected by issuing the following tcpdump command:

```
# tcpdump -e host ip-address
```

Tcpdump will output decoded protocol information for the specified IP address, along with the link-level headers for each captured packet. The output information must be examined to see whether or not two different MAC addresses attempt to make use of the same IP address.

- **ARP Errors**—ARP errors and misconfigurations can be detected by issuing the following tcpdump command:

```
# tcpdump arp
```

Tcpdump will output any decoded ARP information captured from the network. Excessive “who-has” requests can be indicative of ARP misconfiguration problems.

- **Routing Problems**—Data routing problems can be detected by using the following tcpdump command:

```
# tcpdump icmp
```

Tcpdump will output any decoded ICMP protocol information captured from the network. ICMP error messages such as host unreachable can be indicative of routing misconfigurations or other network reachability problems.
