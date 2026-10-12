containing the string: Host switch.home.com (10.0.2.60) appears to be up ... good. Note that the most important point with respect to this example is that nmap is very smart about probing non-existent or down systems; it didn't spend much time or resources probing unresponsive systems. Before nmap attempts to scan a device, it first determines if it is reachable on the network by performing a ping on it. This not only reduces the amount of time required to perform the scan and lessens system resources needed, but it helps to preserve network bandwidth as well. It is important not to underestimate the impact that scanning can have on a network, and nmap does a good job to reduce the network requirements while probing.

# Nmap Output Listing

The listing below shows some of the nmap output when it is used against a series of different computer systems and networking devices. Certainly your mileage may vary, but this tool is quite good at detecting different kinds of systems. This section includes both output and a general description of the systems and supported networking services. Since most of the systems support many of the same networking services and processes, the common ones are listed in Table 5.9.

Table 5.9 Standard nmap network listings

| Port | Service Name | Description |
|---|---|---|
| 7 | echo | Echoes characters sent to this port; service provided by the inetd process; primarily used for testing |
| 8 | discard | Discards any data sent to it; acts like /dev/null for networking services and other networking applications; primarily used for testing |
| 13 | daytime | Provides time in human-readable format; primarily used for testing |