# OffSec

search results. Let's use the latter to activate the module auxiliary/scanner/smb/smb_version index 56.

```
msf6 > use 56
msf6 auxiliary(scanner/smb/smb_version) >
Listing 629 - Activate smb_version module
```

Listing 629 shows we have activated the smb_version module as indicated in the command-line prompt.

To get information about the currently activated module, we can enter info.

```
msf6 auxiliary(scanner/smb/smb_version) > info
Name: SMB Version Detection
Module: auxiliary/scanner/smb/smb_version
License: Metasploit Framework License (BSD)
Rank: Normal
```

Provided by:
hdm <@hdm.io>
Spencer McIntyre
Christophe De La Fuente

Check supported:


Basic options:
Name Current Setting Required Description
--- ------ --------- -----------
RHOSTS yes The target host(s), see
https://github.com/rapid7/metasploit-framework/wiki/Using-Metasploit
THREADS 1 yes The number of concurrent threads (max per
host)

Description:
Fingerprint and display version information about SMB servers.
Protocol information and host operating system (if available) will be reported. Operating system detection requires the remote server to support version 1 of the SMB protocol. Compression and encryption capability negotiation is only present in version 3.1.1.

> Listing 630 - Displaying information about the purpose of the smb_version module

The module description provides information about the purpose of the module as shown in listing 630.

The output also contains the Basic options, which are the arguments for the module. We can also display the options of a module by entering show options. The options contain a column named Required, which specifies if a value needs to be set before the module can be launched. We should note that in most modules, Metasploit will already set the options for us.

```
msf6 auxiliary(scanner/smb/smb_version) > show options
Module options (auxiliary/scanner/smb/smb_version):
Name Current Setting Required Description
```