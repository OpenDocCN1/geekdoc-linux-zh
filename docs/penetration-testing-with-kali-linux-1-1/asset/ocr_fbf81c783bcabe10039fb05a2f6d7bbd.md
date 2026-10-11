![](bbox=[0.31, 0.1, 0.7, 0.24])

*Figure 216. Stack space increased*

As such, ESP points to the $D$ characters (0x44 in hexadecimal) acting as a placeholder for our shellcode:

```
030E7448 41414141 AAAA
030E744C 41414141 AAAA
030E7450 41414141 AAAA
030E7454 42424242 BBBB
030E7458 43434343 CCCC
030E745C 44444444 DDDD
030E7460 44444444 DDDD
030E7464 44444444 DDDD
030E7468 44444444 DDDD
030E746C 44444444 DDDD
...
030E745C 44444444 DDDD
```

*Listing 353 - Increased stack space for shellcode*

This little trick has provided us with significantly more space to work with. Upon further examination, we notice that we now have a total of 704 bytes (0x030E771C - 0x030E745C = 704) of free space for our shellcode.

Also, notice that the address of ESP changes every time we run the exploit, but still points to our buffer. We will address this in a following section, but first we have another hurdle to overcome.

# 11.2.5 Checking for Bad Characters

Depending on the application, vulnerability type, and protocols in use, there may be certain characters that are considered “bad” and should not be used in our buffer, return address, or shellcode. One example of a common bad character, especially in buffer overflows caused by unchecked string copy operations, is the null byte, 0x00. This character is considered bad because a null byte is also used to terminate a string in low level languages such as C/C++. This will cause the string copy operation to end, effectively truncating our buffer at the first instance of a null byte.

In addition, since we are sending the exploit as part of an HTTP POST request, we should avoid 0x0D, the return character, which signifies the end of an HTTP field (in this case the username).

An experienced exploit developer will always check for bad characters. One way to determine which characters are bad for a particular exploit is to send all possible characters, from 0x00 to 0xFF, as part of our buffer, and see how the application deals with these characters after the crash.

To do this, we will repurpose the proof of concept script and replace our D’s with all possible hex characters, except 0x00. (Listing 354):