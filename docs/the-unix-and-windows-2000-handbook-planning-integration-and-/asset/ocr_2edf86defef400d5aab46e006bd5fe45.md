| Variable | Value | Description |
|---|---|---|
| os level | Number | Specifies the priority the SAMBA server will have in winning browse master elections. The higher you set this number (max. 33), the more likely it is the SAMBA server will win the election. We recommend setting this parameter to 0, unless no NT server is available. |
| name resolve order | String | Specifies the order in which the SAMBA server will resolve NetBIOS names. The most common resolve order is wins lmhosts host. |
| wins support | yes/no | Specifies whether or not the SAMBA server will also provide NetBIOS name resolution capabilities. Unless an NT server is not available, do not enable this on your Windows NT network. |
| wins server | IP address | Specifies the server to query for WINS requests. |
| wins proxy | yes/no | Specifies whether or not the SAMBA server will serve as a WINS proxy for non-WINS-enabled clients, such as UNIX workstations not running SAMBA. |
| lm announce | yes/no | Specifies whether or not the SAMBA server will make LanManager announcements to the network. Unless you have legacy LanManager clients on your network, set this parameter to no. |
| dns proxy | yes/no | Specifies whether or not the SAMBA server will serve as a DNS proxy. |

You can also explicitly create any share under a [<sharename>] section and configure it however you wish. You can use any of the allowed variables as specified in the SAMBA documentation. Following is a more complete version of the smb.conf file discussed earlier, including share and printer definitions: