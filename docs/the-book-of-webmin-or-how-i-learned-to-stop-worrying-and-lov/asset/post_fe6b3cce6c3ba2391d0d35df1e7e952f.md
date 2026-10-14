
## 5
GENERAL SYSTEM CONFIGURATION

- Usrmin Configuration ............................................ 40
- Usrmin Module Configuration ............................................ 40
- Available Modules ............................................ 48
- When to Use Usrmin ............................................ 48
- Bootup and Shutdown ............................................ 52
- Disk and Network Filesystems ............................................ 52
- Linux Native Filesystem Mount Details ............................................ 53
- Linux Advanced Mount Options ............................................ 54
- Solaris Filesystem Options ............................................ 56
- Solaris Advanced Mount Options ............................................ 57
- System Documentation ............................................ 58
- System Documentation Search ............................................ 58
- Searching Documentation from Another Module ............................................ 59
- Process Manager ............................................ 60
- Scheduled Commands ............................................ 61
- Scheduled Cron Jobs ............................................ 61
- Software Packages ............................................ 62
- Introduction to Package Managers ............................................ 62
- Supported Operating Systems ............................................ 63
- Using the Package Manager ............................................ 63
- System Logs ............................................ 65
- Adding a System Log ............................................ 66
- Users and Groups ............................................ 67
- Users and Groups Module Configuration ............................................ 68
- Creating a New User ............................................ 75

## 6
SERVER AND DAEMON CONFIGURATION

Introduction to Servers ............................................ 83

## 7
APACHE WEBSERVER

- Global Configuration ............................................ 86
- Processes and Limits ............................................ 86
- Maximum headers in request ............................................ 87
- Maximum request header size ............................................ 87
- Maximum request line size ............................................ 87
- Maximum concurrent requests ............................................ 87
- Maximum requests per server process ............................................ 88
- Maximum spare server processes ............................................ 88
- Minimum spare server processes ............................................ 88
- Initial server processes ............................................ 89
- Display extended status information ............................................ 89
- Networking and Addresses ............................................ 89
- Listen on addresses and ports ............................................ 90
- Multiple requests per connection ............................................ 90
- Keep-alive timeout ............................................ 91
- Listen queue length ............................................ 91
- Addresses for name virtual servers ............................................ 91
- TCP send buffer size ............................................ 91
- Request timeout ............................................ 92
- Apache Modules ............................................ 92
- About Apache Modules ............................................ 93
- MIME Types ............................................ 96
- Miscellaneous ............................................ 96
- Core dump directory ............................................ 96
- Server lock file ............................................ 97
- Server PID file ............................................ 97
- Shared memory scoreboard file ............................................ 97
- Server HTTP header ............................................ 97
- Server execution ............................................ 97
- CGI Programs ............................................ 97
- CGI Script log ............................................ 98
- Maximum logged post data size ............................................ 98
- Maximum CGI log post size ............................................ 98
- Variables set based on browser type ............................................ 98
- Variable set based on request headers ............................................ 98
- Per-Directory Options Files ............................................ 98
- Virtual Servers ............................................ 98
- Log Files ............................................ 99
- Document Options ............................................ 102
- Error Handling ............................................ 105
- User and Group ............................................ 105
- Aliases and Redirects ............................................ 105
- Directory Indexing ............................................ 107
- Imagemaps ............................................ 110
- Proxying ............................................ 111
- Server Configuration ............................................ 113
- Tutorial: A Basic Apache Configuration ........................................ 114
- Configuring Apache Paths ............................................ 114
- Module Selection ............................................ 115
- Adding Content ............................................ 115
- Starting Apache ............................................ 115
- Tutorial: Name-Based Virtual Hosting with Apache ........................................ 116
- Converting a Default Server to a Virtual Server ........................................ 116
- Adding Other Virtual Server Names ............................................ 118

## 8
BIND

- A Brief History of BIND ............................................ 120
- Walking Through an Example Query ............................................ 120
- The BIND Module ............................................ 121
- Global Server Options ............................................ 122
- Other DNS Servers ............................................ 122
- Logging and Errors ............................................ 123
- Access Control Lists ............................................ 124
- Files and Directories ............................................ 125
- Forwarding and Transfers ............................................ 125
- Addresses and Topology ............................................ 126
- Miscellaneous Options ............................................ 127
- Control Interface Options ............................................ 128
- DNS Keys ............................................ 129
- Installing a Key ............................................ 129
- Creating a Key with dnssec-keygen ............................................ 129
- Zone Defaults ............................................ 130
- Refresh time ............................................ 130
- Transfer retry time ............................................ 130
- Defaults for new master zones ............................................ 131
- Default time-to-live ............................................ 131
- Template records ............................................ 131
- Default Zone Settings ............................................ 132
- Existing DNS Zones ............................................ 133
- Zone Types ............................................ 133
- Creating a New Zone ............................................ 133
- Creating a Forward Master Zone ............................................ 133
- Creating a Reverse Master Zone ............................................ 135
- Adding Records to a Master Zone ............................................ 136
- Creating a Slave or Stub Zone ............................................ 139
- Creating a Forward Zone ............................................ 139
- Tutorial: Setting Up a Caching Name Server with BIND ........................................ 140
- Initializing the named.conf ............................................ 140
- Adding Forwarders ............................................ 140
- Tutorial: Name Resolution for Virtual Hosts ........................................ 140
- Create a New Master Forward Zone ............................................ 141
- Adding Address Records ............................................ 141
- Adding an Mail Server Record for Mail ........................................ 142
- Adding a Name Alias ............................................ 142
- Creating an MX Record ............................................ 142
- Applying Changes and Testing the Results ........................................ 143
- Troubleshooting BIND ............................................ 145
- Using Host ............................................ 145
- Using dig ............................................ 147
