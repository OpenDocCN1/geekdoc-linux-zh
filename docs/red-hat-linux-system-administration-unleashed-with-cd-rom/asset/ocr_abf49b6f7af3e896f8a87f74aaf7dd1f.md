Table 14.4 continued

| Type | Name | Purpose |
|------|------|---------|
| HINFO | Host Information | Describes a host's hardware and operating system. |
| WKS | Well-Known Service | Advertises which network services run on a machine. |
| TXT | Text | Stores arbitrary text strings. |

A DNS Resource Record consists of the following items, in order.

+   - **Name**—This is the name of the host or domain referenced by this RR. It is treated relative to the current domain unless it ends with a dot. It may be omitted, in which case the record applies to the last named domain object. This allows several records to be specified for the same domain with a minimum of repetition.
+   - **Time-to-live (TTL)**—This is the length of time, in seconds, that the information in this RR should be kept in a remote cache. It is usually left blank, in which case the default TTL is used, as set in the SOA record.
+   - **Class**—This is usually IN, for Internet.
+   - **Type**—Identifies the type of RR. Normally one of the standard types listed in the table above.
+   - **Data**—This is the actual information stored for this record. For example, in an A record, this is the numeric IP address, and in a PTR record, this is the name corresponding to that address.

# Network Information Service

The Network Information Service, or NIS, is an administrative database system developed by Sun Microsystems. It was formerly called YP (for Yellow Pages), and even though a conflicting trademark forced it to be renamed, the abbreviation YP is still visible. NIS allows important administrative files to be controlled centrally, and distributed around the local area network automatically.

NIS allows network queries to databases that contain data normally held in standard UNIX files; these databases are called NIS maps. The files for which NIS holds maps include /etc/hosts and /etc/networks. NIS is like DNS in that they both provide a means of overcoming the limitations of a network-wide static host table, but NIS is not an alternative to DNS for Internet hosts. Few systems will therefore use NIS without also using DNS for Internet name services.