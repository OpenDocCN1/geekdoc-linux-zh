The initial set of root nameservers is specified using a "hint zone". When the server starts up, it uses the root hints to find a root nameserver and get the most recent list of root nameservers. If no hint zone is specified for class IN, the server uses a compiled-in default of root servers hints. Classes other than IN have no built-in defaults.

# 6.2.22.2. Class

The zone's name may optionally be followed by a class. If a class is not specified, class IN (for Internet), is assumed. This is correct for the vast majority of cases.

The hesiod class is named for an information service from MIT's Project Athena. It is used to share information about various systems databases, such as users, groups, printers and so on. The keyword HS is a synonym for hesiod.

Another MIT development is CHAOSnet, a LAN protocol created in the mid-1970s. Zone data for it can be specified with the CHAOS class.

# 6.2.22.3. Zone Options

allow-notify

See the description of allow-notify in Section 6.2.14.3

allow-query

See the description of allow-query in Section 6.2.14.3

allow-transfer

See the description of allow-transfer in Section 6.2.14.3.

allow-update

Specifies which hosts are allowed to submit Dynamic DNS updates for master zones. The default is to deny updates from all hosts.

update-policy

Specifies a "Simple Secure Update" policy. See Section 6.2.22.4.