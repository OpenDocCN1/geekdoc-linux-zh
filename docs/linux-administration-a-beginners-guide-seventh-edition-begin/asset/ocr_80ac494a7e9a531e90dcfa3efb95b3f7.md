# CHAPTER 8 Core System Services 225

v6only = no
groups = yes
umask = 002

```
}includedir /etc/xinetd
```

The first line of our sample xinetd.conf is a comment explaining what the file is and what it does.

After the comments, you see the first block: defaults. The first attribute that is defined in this block is log_type, which is set to the value SYSLOG daemon info. Nine attributes in total are defined in this block, the last one being umask. Since this block is titled defaults, the variables that are set within it will apply to all future blocks that are defined. We'll list the attributes and values describing their meaning in the next section.

Finally, the last line of the file specifies that the /etc/xinetd.d directory must be examined for other files that contain more information. This will cause xinetd to read all the files in the directory and parse them as if they were part of the /etc/xinetd.conf file.

# Attributes and Their Meanings

Table 8-3 lists some of the attribute/variable names that are supported in the /etc/xinetd.conf file.

| Variable | Description |
|---|-|
| id | This attribute is used to identify a service uniquely. This is useful, because services exist that can use different protocols and that need to be defined with different entries in the configuration file. By default, the service ID is the same as the service name. |
| type | Any combination of the following values may be used: RPC if this is a Remote Procedure Call (RPC) service, INTERNAL if this service is provided by xinetd, or UNLISTED if this is a service not listed in the /etc/services file. |
| disable | This is either yes or no. A yes means that although the service is defined, it is not available for use. |
| socket type | Valid values for this variable are stream, which indicates that this service is a stream-based service; dgram, which indicates that this is a datagram; or raw, which indicates that this service uses raw IP packets. The stream value refers to connection-oriented TCP streams (for example, Telnet and FTP), the dgram refers to datagram (User Datagram Protocol [UDP]) streams for example, the File Transfer Protocol [TFTP] service is a datagram-based protocol). Other protocols outside the scope of TCP/IP do not, but you'll rarely encounter them. |

Table 8-3 xinetd Configuration File Attributes