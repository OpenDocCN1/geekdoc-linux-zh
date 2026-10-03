you configure). The most popular SSH server is OpenSSH’s sshd.

# SSH Clients

Use an SSH client to connect to your remote server or network device. The most popular SSH client for Windows systems is PuTTY. The standard SSH client for Unix-like systems is ssh(1), from OpenSSH. Both are freely available and usable for any purpose, commercial or noncommercial, at no cost.

Microsoft also recently forked OpenSSH to include an SSH client in Windows. It’s considered experimental, though, and development is continuing. Experiment with it as you wish; it should work much like OpenSSH. It’s also part of Windows’ Linux subsystem. If you’re using a Windows-native SSH, though, you really want to use PowerShell rather than the traditional terminal.

Once you understand PuTTY and OpenSSH, you’ll have the base knowledge to use any secure SSH client.

# SSH Protocol Versions

The SSH protocol comes in two versions, SSH-1 (version 1) and SSH-2 (version 2). Always use SSH-2. All modern SSH software defaults to version 2. You will find old embedded devices that still rely on SSH version 1, but SSH-1 is barely more secure than unencrypted telnet.

One person designed SSH-1 for his own needs. It met those needs admirably, and in the 1990s it was a whole bunch better than telnet. As SSH grew more popular, more people examined the protocol and exposed weaknesses in the original design. With today’s computing power, SSH-1 is highly vulnerable to attacks. While SSH-1 encrypts your data in transit and prevents casual eavesdropping, an attacker that knows a couple tricks can capture your data, decrypt your data in transit, lull you into thinking that you logged on to the correct machine when you are actually connected to a different host, insert arbitrary text into the data stream, or any combination of these. Attacking an SSH-1 data stream isn’t quite a point-and-click process, but intruders do break SSH-1 in the real world.

The appearance of security is worse than no security. Never use SSH version 1.

It might seem harmless to permit SSH-1 for servers or clients that don’t support SSH-2. The client and server transparently negotiate the SSH version they will use for a connection however. If either client or server tolerates SSH-1, an intruder can capture your login credentials and all transmitted data. It’s fairly straightforward to insert arbitrary text (such as rm -rf /*) into an SSH-1 session. This was discovered in 1998, and today’s massive computing power has made this attack far easier. SSH-1 sessions can be decoded in real time by programs