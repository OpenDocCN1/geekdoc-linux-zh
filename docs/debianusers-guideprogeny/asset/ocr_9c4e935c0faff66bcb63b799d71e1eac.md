# Creating the Global Configuration File (global.cfg)

The global.cfg file contains the master information for the automated install. One option is entered per line. When an option requires a value, leave a space between the option and the value.

# Options for the global.cfg File

| Option | What It Does |
| --- | --- |
| baseurl | The URL for the minimal system’s tar file. The URL can be a CD (cdrom:) or a web address (http://). This option is required. |
| rootpwd | The password hash for the root user. This option is required |
| nosafe | Continues the install, even if a filesystem exists on the target machine. |
| network | Allows the automated installer to configure the network. Possible values are: ▼ dhcp: Use DHCP. ▼ netdb: configure using the network.cfg file. ▼ none: do not configure the network. |