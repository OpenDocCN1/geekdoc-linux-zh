The netstat Trojan hides network connections. With the network connections (e.g., telnet and ftp) hidden, the intruder is free to pick up the bounty of sniffed passwords or use your site as a springboard from which to attack other sites.

The ifconfig Trojan hides the fact that your network interface is in promiscuous mode. There is no config file associated with the ifconfig Trojan.

The ps Trojan hides running processes belonging to a specified UID, TTY, or program name. Many of the Trojans have an added "showall" option (-/) that ignores the contents of the mask file.

# Mask File Formats

# ps Mask File

The following is an example /dev/ptyp mask file.

```
0 0      # Strips all output with processes running under root
1 p0     # Strips all output associated with tty typ0
2 sniffer # Strips from output all programs with the name sniffer
```

Only the first 125 characters in a line are significant. strtok(3) is used to parse a line of input, and no error checking is done on the format or number of fields. One result is that a blank line in the file will most probably cause a segmentation violation. Only the first two fields in a line are looked at; so, even though comments are not explicitly supported, they are benign. As shown above, there are three types of specifications. A specification other than 0, 1, or 2 will be ignored. With specification 2, only the name of a program is checked, not options or arguments that would be seen with ps -w.

# netstat Mask File

The SunOS and Linux versions use slightly different encodings for masking actions. The following are examples for each type of /dev/ptypq mask file. (Note that foreign refers to connections from the local host out, and local refers to connections into the local host.)

# SunOS Rootkit

```
0 6667       # Strip all foreign irc network connections (port #)
1 23         # Strip all local telnet connections (port #)
2 192.88.209.5 # Strip all foreign connections from cert.org
3 128.120.1.  # Strip all local connections to a ucd subnet
```