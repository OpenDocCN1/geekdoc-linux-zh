File Sharing 525

```
preferred master = No
domain master = No
hosts allow = 192.168.34.elm
```

These options mean the following:

+   - workgroup: Windows networks are organized into workgroups, which are collections of computers sharing the same workgroup parameter. This name is specified by the workgroup parameter. If you don't set this parameter to match your network's workgroup, you may not be able to access the Samba server. (Many Windows networks use domains rather than workgroups. Domains also have names that you set using the group parameter).
- netbios name: A computer's NetBIOS name is the name by which other computers know it, and the netbios name sets this feature. If this parameter is not set, Samba takes the default value from the computer's machine name; for instance, ginko.threeonline.com becomes GINGKO.
- server string: This parameter sets a comment that's visible when you browse a workgroup using the Windows Network Neighborhood tool. It's purely a cosmetic feature of Windows networking.
- encrypt passwords: This parameter is critically important, and it causes a great deal of trouble to new Samba administrators. By default, Samba accepts only cleartext passwords, which are transmitted without encryption. This characteristic is a security risk, however; it's better to transmit passwords in an encrypted form, which makes it difficult or impossible to decipher an intercepted password. Using encrypted passwords on Samba, however, requires maintaining a separate Samba-only password list. (Samba checks cleartext passwords against Linux's normal database.) Early versions of Windows 95 and Windows NT 4.0 used cleartext passwords, but Windows 95 OSR 2, Windows NT 4.0 SP 3, and all later versions of Windows use encrypted passwords. The section “Setting Password Options” describes Samba's encrypted password handling in more detail.

![](bbox=[0.938, 0.733, 0.996, 0.833])