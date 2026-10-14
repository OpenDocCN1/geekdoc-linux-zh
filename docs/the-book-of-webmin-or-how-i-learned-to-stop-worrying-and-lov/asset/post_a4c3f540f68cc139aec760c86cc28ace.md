
Timeout on waiting for answer to MAIL FROM .................................... 186
Timeout on waiting for answer to RCPT TO .................................... 186
Timeout on waiting for answer to DATA .................................... 186
Timeout on waiting for answer to transmit of message content .................................... 186
Timeout on waiting for answer to ending "." .................................... 187
Timeout on waiting for answer to QUIT .................................... 187
Delivery Rates .................................... 187
Max number of parallel deliveries to the same destination .................................... 187
Max number of recipients per message delivery .................................... 187
Initial concurrency level for delivery to the same destination .................................... 187
Max time [days] in queue before message is undeliverable .................................... 187
Min time [secs] between attempts to deliver a deferred message .................................... 187
Max time [secs] between attempts to deliver a deferred message .................................... 188
Time [secs] between scanning the deferred queue .................................... 188
Transports that should not be delivered .................................... 188
Debugging Features .................................... 188
List of domain/network patterns for which verbose log is enabled .................................... 188
Verbose logging level when matching the above list .................................... 188
Postfix, Unsolicited Commercial Email, and Access Controls .................................... 188
Access Control List Order .................................... 189
Tutorial: Setting Up a Basic Postfix Mail Server .................................... 190
Tutorial: Virtual Hosting Email with Postfix .................................... 191

## 11
SENDMAIL

Configuring Sendmail .................................... 194
The Sendmail Module .................................... 194
Options .................................... 195
Send outgoing mail via host .................................... 195
Forward unqualified usernames to host .................................... 195
Forward mail for local users to host .................................... 195
Delivery mode .................................... 196
Max load average for sending .................................... 196
Max load average for receiving .................................... 196
Max child processes .................................... 196
Max connections/second .................................... 196
Min time before retrying send .................................... 196
Maximum queue size .................................... 197
Time before giving up .................................... 197
Time before sending warning .................................... 197
Mail queue directory .................................... 197
Send error messages to .................................... 197
User forward files .................................... 197
Min free disk space .................................... 198
Max message size .................................... 198
Log level .................................... 198

## 12
SQUID

- MIME-encode bounce messages? 198
- File security options 198
- Other Support Files 199
  - Mail Aliases 199
  - Local Domains 200
  - Domain Masquerading 200
  - Trusted Users 200
  - Address Mapping 200
  - Domain Routing 201
  - Outgoing Addresses (Generics) 201
  - Outgoing Domains 202
  - Domain Mapping 202
  - Spam Control 202
  - Relay Domains 203
  - Mail Queue 203
  - User Mailboxes 203
- Editing the m4 Configuration File 203
  - Adding a Feature 204
- Tutorial: Setting Up Sendmail 205
  - Configuring Domains to Receive Mail For 205
  - Permitting Local Users to Relay 205
- Tutorial: Virtual Hosting Email with Sendmail 206
  - Adding Address Mapping Entries 206

- Ports and Networking 208
  - Proxy port 209
  - ICP port 209
  - Incoming TCP address 209
  - Outgoing TCP address 209
  - Incoming UDP address 209
  - Outgoing UDP address 209
  - Multicast groups 209
  - TCP receive buffer 210
- Other Caches 210
  - Internet Cache Protocol 210
  - Parent and Sibling Relationships 210
  - When to Use ICP 210
  - Other Proxy Cache Servers 212
  - Edit Cache Host 212
  - Cache Selection Options 215
- Memory Usage 216
  - Memory usage limit 216
  - FQDN cache size 217
  - Memory high water mark, Memory low water mark 217

- Disk high-water mark, Disk low-water mark ................................................ 217
- Maximum cached object size ................................................ 217
- IP address cache size, IP cache high-water mark, IP address low-water mark ... 217
- Logging ................................................ 217
- Access log file ................................................ 218
- Debug log file ................................................ 219
- Storage log file ................................................ 219
- Cache metadata file ................................................ 220
- Use HTTPD log format ................................................ 220
- Log MIME headers ................................................ 220
- Perform RFC931 ident lookups for ACLs ................................................ 220
- RFC931 ident timeout ................................................ 220
- Log full hostnames ................................................ 220
- Logging netmask ................................................ 221
- Debug options ................................................ 221
- MIME headers table ................................................ 221
- Cache Options ................................................ 221
- Cache Directories ................................................ 221
- Other Cache Options ................................................ 222
- Helper Programs ................................................ 225
- FTP column width ................................................ 226
- Anon FTP login ................................................ 226
- Squid DNS program ................................................ 227
- Number of DNS programs ................................................ 227
- Append domain to requests ................................................ 227
- DNS server addresses ................................................ 227
- Cache clearing program ................................................ 227
- Squid ping program ................................................ 227
- Custom redirect program, Number of redirect programs ................................................ 228
- Custom Authentication program, Number of authentication programs ................................................ 228
- Authentication Programs ................................................ 229
- Basic and Digest Authentication Options ................................................ 230
- NTLM authentication options ................................................ 231
- Access Control ................................................ 231
- Access Control Lists ................................................ 232
- Available ACL Types ................................................ 234
- Administrative Options ................................................ 237
- Run as Unix user and group ................................................ 237
- Proxy authentication realm ................................................ 237
- Cache manager email address ................................................ 238
- Visible hostname ................................................ 238
- Unique hostname ................................................ 238
- Cache announce host, port, and file ................................................ 238
- Announcement period ................................................ 238
- Miscellaneous Options ................................................ 238
- Startup DNS test addresses ................................................ 238
- SIGUSR1 logfile rotations ................................................ 239
- Default domain ................................................ 239
- Error messages text ................................................ 239
