```
amiee::526::Amiee'S-Account:/cygdrive/d:/ssh/switch.exe
amit::527::Amit's-Account:/cygdrive/d:/ssh/switch.exe
katie::528::Katie's-Account:/cygdrive/d:/ssh/switch.exe
rohan::529::Rohan's-Account:/cygdrive/d:/ssh/switch.exe
shreya::530::Shreya's-Account:/cygdrive/d:/ssh/switch.exe
shaashi::531::Shaashi's-Account:/cygdrive/d:/ssh/switch.exe
prabha::532::Prabha's-Account:/cygdrive/d:/ssh/switch.exe
chandrathar::533::Chandrathar's-Account:/cygdrive/d:/ssh/switch.exe
```

3. Stop and restart the OpenSSH service using the following commands:
```
c:\net stop "OpenSSH Server"
c:\net start "OpenSSH Server"
```

Now the Windows file server has an OpenSSH server running on the system, with all users in the engineering group having access to the D partition.

![](bbox=[0.1, 0.38, 0.9, 0.78])