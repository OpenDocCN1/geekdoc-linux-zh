separated by pipes (|) and includes a series of instructions for executable files to be replaced. The thread now searches the system for each file listed in the state ment file and saves it as [FILE_NAME], a.

Finally, the thread replaces the original files with the newly obtained S06 filter module and makes it executable. All of these steps allow threat actors to put wrappers around specific executable system files.

Thread #4 monitors and logs logged-in users. If a user is logged on to the Linux machine and their IPv4 does not

match a local IPv4 or one of the C2s, its details are logged and sent to the C2 server.

Thread #5 takes care of cleaning up old reverse shell sessions. First of all, the thread monitors reverse shell sessions. If a reverse shell session is found that has not been active for almost an hour, the session is removed.

# ## C2 Communication

Before C2 communication begins, two global structures are checked: One contains the configuration value that specifies whether TCP or UDP should

be used when connecting to C2; the other specifies whether C2 communication should be interrupted if there are logged-in users. If one of these checks fails, the malware does not establish communication with C2. If the checks are successful, the backdoor analyzes the C2 address and resolves a C2_domain to IPv4 if necessary.

Next, the malware sets up a socket in TCP or UDP mode, depending on the configuration, and attempts to establish a connection to the C2 server. If the connection is successful, the malware starts a thread to parse C2 commands. After

**Table 3: Supported Functions**

| ID | Description | Parameters | Existing in the Windows version |
|---|---|---|---|
| 0x02 | List files and directories under a specific folder | Name of the folder | yes |
| 0x03 | List files and directories in a specific folder | List of files or directories separated by && | yes |
| 0x05 | Send files to C2 | Request ID, file list separated by && | yes |
| 0x06 | Terminate the “Send files” command | – | yes |
| 0x08 | Download a file from C2 and execute (if a flag is activated) | Execute flag, file name, file data, all separated by /t | yes |
| 0x09 | Terminate the “Download files” command | – | yes |
| 0x0E | Update the C2 URL | List of C2 URLs, separated by /t | yes |
| 0x0F | Display logged-in users | – | yes |
| 0x11 | List running processes | – | yes |
| 0x12 | End process | Process ID to be terminated | yes |
| 0x13 | List executed services | – | yes |
| 0x14 | Start/stop service | Service name, action type, separated by /t; action types: 1 – Start service, 0 – Stop service, 2 – Stop and delete service | yes |
| 0x18 | Execute process and send back the response | Process path to be executed | yes |
| 0x19 | Make file executable and execute | Receive multiple files to be executed, separated by /t | yes |
| 0x1A | Start/stop/call up status of HTTP proxy | Integer value | no |
| 0x1B | Start reverse shell | – | yes |
| 0x1C | Undo shell restart | – | no |
| 0x1D | Undo shell termination | – | no |
| 0x1E | Write to reverse shell | Binary values divided by 0x010x02 | yes |
| 0x27 | Rename, copy, move file | Action type, file path, new path | yes |
| 0x28 | Send ok to C2 | – | yes |
| 0x2B | Change proxy connection type | Integer value | yes |
| 0x2C | Set proxy type | Integer value | yes |
| 0x2D | Change file transfer mode | Integer, integer value | yes |
| 0x2E | Auto-complete uninstall, remove persistence, terminate parent daemon and exit | – | yes |
| 0x31 | Update a global integer value used as the UDP packet length | Integer value | yes |
| 0x32 | Read file and return content | File path, max. bytes to be read | no |
| 0x33 | Write data to file | File path, bytes to be written to a hexadecimal character string | no |
| 0x34 | Collect user activities from various files such as /var/run/utmp, var/log/utmp, var/log/lastlog | – | no |
| 0x35 | Analyze and send /usr/lib/i18n/gettext/ a file | – | no |
| 0x36 | Analyze data and write to /usr/lib/i18n/gettext/a file | Fields separated by /t | no |