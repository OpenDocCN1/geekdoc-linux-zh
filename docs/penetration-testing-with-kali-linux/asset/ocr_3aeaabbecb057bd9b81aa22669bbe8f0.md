# 14.1.2 Importing and Examining the Exploit

In this example, we'll target Sync Breeze Enterprise 10.0.28 and focus on one of the two available exploits. This will provide us with a working exploit for our target environment and allow us to walk through the modification process.

Searching by product and version, we'll notice that one of the available exploits for this particular vulnerability is coded in C.

```
kali@kali:~$ searchploit "Sync Breeze Enterprise 10.0.28"
```

| Title | | |
|---|---|---|
| Sync Breeze Enterprise 10.0.28 | Denial-of-Service (PoC) | windows/dos/43200.py |
| Sync Breeze Enterprise 10.0.28 | Remote Buffer Over | exploits/windows/remote/42928.py |
| Sync Breeze Enterprise 10.0.28 | Remote Buffer Over | exploits/windows/dos/42341.c

Listing 311 - Searching for available exploits for vulnerability software using searching

Denial of Service (DoS) results results in a simple crash and no exploit exploit path. We should ideally avoid DoS exploits whenever we have better alternatives, in our case. Let's focus on the last two entries.

The vulnerability is present in the HTTP server module where a buffer overflow condition is triggered on a POST request. While we reading the entire Python code, the core functionality of the exploit script can be summarized using the following code:

```
offset = "A" * 780
jMP_ESP = "\x83\x0c\x09\x10"
shellcode = "\x90" * 16 + msf_shellcode
exploit = offset + JMP_ESP + shellcode
```

Listing 312 - Sync Breeze 10.0.28 ESP instruction's Summary

At 780, we overwrite the instruction pointer with a JMP ESP instruction located at the memory address 0x1090c83. Next, we add the shellcode with 16 NOPs. The exploit buffer is included in the HTTP request and sent.

Since we're more familiar with how the vulnerability works and how it is exploited, let's briefly review the differences between scripting languages such as Python and a compiled language as C.

While there are plenty of differences between the two languages, we will focus on two main differences that affect us, memory management and string operations.

The first key difference is that scripting languages are executed through an interpreter and not compiled to create a stand-alone executable. Because scripting languages require an interpreter, we cannot run a Python script in an environment where Python is not installed. This could limit us in the field, especially if we need to run a stand-alone (like a local privilege escalation) that must run in an environment that doesn't have Python pre-installed.