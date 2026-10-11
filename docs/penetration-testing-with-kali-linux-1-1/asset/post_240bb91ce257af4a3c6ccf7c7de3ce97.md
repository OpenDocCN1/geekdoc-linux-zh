
## 15.1.1 Overview and Considerations

The general flow of a standard stack overflow (in applications running in user mode without mitigations such as DEP and ASLR) is fairly straight-forward. The exploit will:

- Create a large buffer to trigger the overflow.
- Take control of EIP by overwriting a return address on the stack by padding the large buffer with an appropriate offset.
- Include a chosen payload in the buffer prepended by an optional NOP sled.
- Choose a correct return address instruction such as JMP ESP (or different register) in order to redirect the execution flow into our payload.

Additionally, as we fix the exploit, depending on the nature of the vulnerability, we may need to modify elements of the deployed buffer to suit our target such as file paths, IP addresses and ports, URLs, etc. If these modifications alter our offset, we must adjust the buffer length to ensure we overwrite the return address with the desired bytes.

Although we could trust that the return address used in the exploit is correct, the more responsible alternative is to find the return address ourselves, especially if the one used is not part of the vulnerable application or its DLLs. One of the most reliable ways to do this is to clone the target environment locally in a virtual machine and then use a debugger on the vulnerable software to obtain the memory address of the return address instruction.

We must also consider changing the payload contained in the original exploit code.

As mentioned in a previous module, public exploits present an inherent danger because they often contain hex-encoded payloads that must be reverse-engineered to determine how they function. Because of this, we must always review the payloads used in public exploits or better yet, insert our own.

When we do this, we will obviously include our own IP address and port numbers and possibly exclude certain bad characters, which we can determine on our own or glean from the exploit comments.

While generating our own payload is advised whenever possible, there are exploits that use custom payloads that are key for a successful compromise of the vulnerable application. If this is the case, our only option is to reverse engineer the payload to determine how it functions and if it is safe to execute. This is difficult and beyond the scope of this module, so we will instead focus on shellcode replacement.

All of these considerations must be kept in mind as we re-purpose the exploit.

## 15.1.2 Importing and Examining the Exploit

In this example, we will again target Sync Breeze Enterprise 10.0.28 as we did in a previous module, but we will focus on a different exploit. This will provide us with another working exploit for our target environment and allow us to walk through the modification process.

Searching by product and version, we notice that there are two available exploits for this particular vulnerability, one of which is coded in C:

```bash
kali@kali:~$ searchsploit "Sync Breeze Enterprise 10.0.28"
```

| Exploit Title | Path (/usr/share/exploitdb/) |
| :--- | :--- |
| Sync Breeze Enterprise 10.0.28 - Remote Buffer Over | exploits/windows/remote/42928.py |
| Sync Breeze Enterprise 10.0.28 - Remote Buffer Over | exploits/windows/dos/42341.c |

Listing 426 · Searching for available exploits for our vulnerable software using searchsploit

Since we’re already familiar with how the vulnerability works and how it is exploited, we are presented with a good opportunity to see the differences between scripting languages such as Python and a compiled language such as C without the added complexity of unraveling a new vulnerability.

While there are plenty of differences between the two languages, we will focus on two main differences that will affect us, including memory management and string operations.

The first key difference is that scripting languages are executed through an interpreter and not compiled to create a stand-alone executable. Because scripting languages require an interpreter, this means that we can not run a Python script in an environment where Python is not installed. This could limit us in the field, especially if we need a stand-alone exploit (like a local privilege escalation) that must run in an environment that doesn’t have Python pre-installed.

> As an alternative, we could consider using PyInstaller (https://www.pyinstaller.org), which packages Python applications into stand-alone executables for various target operating systems. However, given the nuances of exploit code, we suggest porting the code by hand to fully understand how the exploit will work against the target.

An additional difference between the two languages is that in a scripting language like Python, concatenating a string is very easy and usually takes the form of an addition between two strings:

```python
kali@kali:~$ python
>>> string1 = "This is"
>>> string2 = " a test"
>>> string3 = string1 + string2
>>> print string3
This is a test
```

Listing 427 · String concatenation example in Python

As discussed later in this module, concatenating strings in this way is not allowed in a programming language such as C.

To begin the process of modifying our exploit, we will move the target exploit[380] to our current working directory by using SearchSploit’s handy -m mirror (copy) option:

[380] (Offensive Security, 2017). https://www.exploit-db.com/exploits/42341/

```bash
kali@kali:~$ searchsploit -m 42341
    Exploit: Sync Breeze Enterprise 10.0.28 - Remote Buffer Overflow (PoC)
    URL: https://www.exploit-db.com/exploits/42341/
    Path: /usr/share/exploitdb/exploits/windows/dos/42341.c
File Type: C source, UTF-8 Unicode text, with CRLF line terminators

Copied to: /home/kali/42341.c
```

Listing 428 - Using searchsploit to copy the exploit to the current working directory

Now that the exploit is mirrored to our home directory, we can inspect it to determine what modifications (if any) are required to compile the exploit and make it work in our target environment.

However, before even considering compilation, we notice that the headers (such as **winsock2.h**[381]) indicate that this code was meant to be compiled on Windows:

```c
#include <nttypes.h>
#include <stdio.h>
#include <winsock2.h>
#include <windows.h>
```

Listing 429 - Displaying the C headers at the beginning of the exploit code

Although we could attempt to compile this on Windows, we will instead cross-compile[382] this exploit on Kali.

## 15.1.3 Cross-Compiling Exploit Code

In order to avoid compilation issues, it is generally recommended to use native compilers for the specific operating system targeted by the code; however, this may not always be an option.

There are situations where we only have access to a single attack environment (like Kali), but need to leverage an exploit that is coded for a different platform. This is where a cross-compiler can be extremely helpful.

We will use the extremely popular *mingw-64* cross-compiler in this section. If it's not already present, we can install it with **apt**:

```bash
kali@kali:~$ sudo apt install mingw-w64
```

Listing 430 - Installing the mingw-64 cross-compiler in Kali

After the installation has completed, we can use **mingw-64** to compile the code into a Windows PE file.[383] The first step is to see if the exploit code compiles without errors:

```bash
kali@kali:~$ i686-w64-mingw32-gcc 42341.c -o syncbreeze_exploit.exe
/tmp/syncbreeze_exploit.c:(.text+0x2e): undefined reference to `_imp__WSAStartup@8'
/tmp/syncbreeze_exploit.c:(.text+0x3c): undefined reference to `_imp__WSAGetLastError@0'
/tmp/syncbreeze_exploit.c:(.text+0x80): undefined reference to `_imp__socket@12'
/tmp/syncbreeze_exploit.c:(.text+0x93): undefined reference to `_imp__WSAGetLastError@0'
/tmp/syncbreeze_exploit.c:(.text+0xbd): undefined reference to `_imp__inet_addr@4'
```

[381] (Microsoft, 2018), https://msdn.microsoft.com/en-us/library/windows/desktop/ms737629(v=vs.85).aspx
[382] (Wikipedia, 2019), https://en.wikipedia.org/wiki/Cross-compiler
[383] (Offensive Security, 2015), https://forums.offensive-security.com/showthread.php?t=2206&p=8529
