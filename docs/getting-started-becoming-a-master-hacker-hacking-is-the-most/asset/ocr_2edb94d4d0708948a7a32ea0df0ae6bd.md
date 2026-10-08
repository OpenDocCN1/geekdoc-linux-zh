here is to make it more difficult for the AV application to match anything in this shellcode with its database of known malicious code.

When we hit the TAB key, it lists all the methods available for this shellcode. These encoding methods will differ slightly with different shellcode and obfuscation techniques.

In this case, we will encode it with jsfuck.



```
encode>
base64 rot13 simple_base64_rev simple_hex_rev
jsfuck simple_ascii simple_hex
encode> jsfuck
[+] file "windows7shell" encoded successfully!
```

encode > jsfuck Yes, jsfuck is real encoding scheme. It is seldom used subset of Javascript that is written with just 6 characters ([,],(,),! and +. It can be particulary useful for bypassing web form input validation and obfuscation.

When we hit enter, OWASP-ZSC encodes our shellcode with jsfuck and announces it has completed its task!

**Testing Our Shellcode** The final step is to test your new shellcode against AV software. If you know what AV software the target is using, simply test it against that one (check out my article on recon-ng to determine the AV the target is using). If not, you can test your new shellcode at VirusTotal (www.virustotal.com). It’s important to note that VirusTotal shares your code with the AV developers.