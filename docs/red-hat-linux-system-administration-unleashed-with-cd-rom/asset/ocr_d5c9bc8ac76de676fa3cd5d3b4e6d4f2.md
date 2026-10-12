# TABLE 16.1 continued

| Option | Description |
|---|---|
| `-q` | Outputs less detailed packet decode information per packet. |
| `-r file` | Processes packet data stored in file, instead of capturing data from a live network interface. If file is specified as "-", the stdin file descriptor is used as the input source. |
| `-s length` | Captures up to length bytes of data for each packet that is processed. This option allows network sniffing performance to be optimized by preventing the hosts' packet capture routines from retrieving unwanted data. Capturing only the data that is necessary for analysis tasks helps to prevent packet loss when monitoring high-speed networks. If protocol information contained in a captured packet is truncated as a result of this option a [|proto|] indicator is output, where proto is the protocol layer of the packet in which data truncation occurred. If this command-line option is not given, tcpdump defaults to capturing 68 bytes of data per received packet. |
| `-S` | Prints the true values of transmitted TCP sequence numbers. If this option is not set, tcpdump will attempt to keep track of sequence number state information for TCP virtual circuits, printing sequence number information relative to 0. |
| `-t` | Disables the output of time stamp information for each captured data packet. |
| `-tt` | Outputs an unformatted time stamp for each captured data packet. |
| `-v` | Outputs protocol decode information with a higher level of verbosity. |
| `-vv` | Outputs protocol decode information with the highest level of verbosity available. |
| `-w file` | Writes the captured binary packet data to file. The use of this option will prevent the output of decoded protocol information. If file is specified as "-", the binary packet information is output to stdout. |
| `-x` | Outputs received packet data in hexadecimal format, minus the link-level protocol header. |
| `expression` | Filters captured packets according to expression. Data packets will only be processed and displayed if expression evaluates as true. Details on how to filter incoming traffic are given in the "Analyzing Types of Traffic" section of this chapter. |