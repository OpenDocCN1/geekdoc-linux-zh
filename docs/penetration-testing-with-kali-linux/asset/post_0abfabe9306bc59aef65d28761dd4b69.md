
# OffSec Penetration Testing with Kali Linux

(and TCP window sizes), and these slight variances create a fingerprint that Nmap can often identify.

Nmap will inspect the traffic received from the target machine and attempt to match the fingerprint to a known list. By default, Nmap will display the detected OS if the retrieved fingerprint is very accurate. Since we want to get a rough idea of the target OS, we include the osscan-guess option to force Nmap to guess the result if it is not fully accurate.

For example, let's consider this simple Nmap fingerprint scan.

```
kali@kali~$ sudo nmap -O 192.168.0.54 --oscan-guess
...
Running (GUESSING): Windows Server 2008|2012|2016|Vista (88%)
OS CPE: cpe:microsoft:windows_server:2008:sp1
cpe:microsoft:windows_server:2008:r2 cpe:microsoft:windows_server:2012:r2
cpe:microsoft:windows_server:2016 cpe:microsoft:windows_7
cpe:microsoft:windows_vista:sp1:home_premium
Aggressive (GUESSING): Windows Server 2008 Vista or Windows Server 2008 R2 (88%), Microsoft Windows Server 2012 Windows Server 2012 R2 (88%), Microsoft Windows Server 2012 R2 (88%), Microsoft Windows Server 2016 (87%), Microsoft Windows 7 (86%), Microsoft Windows Vista Home Premium SP1 (85%), Windows 7 Professional (85%)\No exact OS matches for host (If you know what OS is running on, see
https://nmap.org/submit/)
...
```

> Listing 67 - Using nmap for OS fingerprinting

The response suggests that the underlying operating system of this target is either Windows 2008 R2, 2012, 2016, Vista, or Windows 7.

> Note that OS Fingering is not always 100% accurate, often due to network devices like firewalls or proxies that rewrite packet headers in the communication.

Once we have recognized the underlying operating system, we can further identify services running on specific ports by inspecting service banners with -A parameter which also runs various OS and service enumeration scripts against the target.

```
kali@kali~$ nmap -sT -A 192.168.0.54
nmap scan report for 192.168.0.54
Host is up (0.12s latency).
Not shown: 996 closed tcp ports (conf-used)
PORT STATE VERSION
21/tcp open ftp?
| fingerprint-strings:
| DNSStatusRequestTCP, DNSVersionBindReqTCP, GenericLines, NULL, RPCCheck,
SSLSession,TLSSessionReq, TLSServerCookie:
220-Filezilla Server 1.2.0
| Please visit https://filezilla-project.org/
GetRequest:
|220-Filezilla Server 1.2.0
| Please visit https://filezilla-project.org/
```

What are you trying to do? Go away.
Options, RTSRequest:
220-FileZilla Server 1.2.0
Please visit https://filezilla-project.org/
Wrong command.
Help:
220-FileZilla Server 1.2.0
Please visit https://filezilla-project.org/
The following commands are recognized.
USER TYPE SYST BTO RNFR REST QUEST
HELP XXMD MLQ MNQ EPSY XWWD NOUP OPTS DELETE
CDUP APPE STOR ALOE PTRWD FEAT CLNT CLMT
MODE XMRD PROT ADAT ABPR XPWD MDTM MLIS MLSD FEAT CLNT PASV
NLST EPRT PASS STUS PAT COST
Help ok.

```
ftp-stat:
| ssl-cert: Subject: commonName=filezilla-server self signed certificate
| Not valid before: 2022-02-01T15:37:24
| Not valid after: 2023-01-07T15:42:24
| ssl-date: randomness does not represent time
135/tcp open ms-rpc
139/tcp open netbios
445/tcp open microsoft-ds
Nmap done: 1 IP address (host) scanned in 55.6 seconds
```

> Listing 68 - Using nmap for banner grabbing and service enumeration

In this example we use -A parameter to run a service scan with extra options. If we want to run a plain nmap scan we can do it by only the -sV parameter. Banner grabbing significantly impacts the amount of traffic used as well as the speed of our scan. We should always be mindful of the options we use with nmap and how they affect our scans. (img/33d6ea891e7464f1ad6442619ced490.png)

```
kali@kali~$ nmap --script http-headers 192.168.0.50
Starting Nmap 7.92 ( https://nmap.org ) at 2022-03-10 13:53 EST
Nmap scan report for 192.168.0.50
Host is up (0.14s latency).
Not shown: 998 closed tcp ports (conn-refused)
PORT STATE SERVICE
22/tcp open ssh
80/tcp open http
http-headers:
Date: Thu, 10 Mar 2022 18:53 GMT
Server: Apache/2.4.41 (Ubuntu)
Last-Modified: Thu, 10 Mar 2022 18:51 GMT
ETag: "5d9e1b5371240"
Accept-Ranges: bytes
Content-Length: 209
Connection: close
Content-Type: text/html
(Request type: HEAD)
Nmap done: 1 IP address (host) scanned in 5.11 seconds
```

> Listing 69 - Using Nmap's scripting engine (NSE)

To view more information about a script, we can use the --script-help option, which displays a description of the script and a URL where we can find more in-depth information, such as the script arguments and usage examples.

```
kali@kali~$ nmap --script-help http-headers
Starting Nmap 7.92 ( https://nmap.org ) at 2022-03-10 13:54 EST

http-headers
Categories: discovery safe
https://nmap.org/doc/http-headers.html
Performs a HEAD request for the root folder of a web server and displays the HTTP headers.
```

> Listing 70 - Using the --script-help option to view more information about a script

When internet access is not available, much of this information can also be found in the NSE itself. It's our time to explore the various NSE scripts, as many of them are helpful and time-saving. Having learned how to perform port scanning from Kali, let's explore how we can apply the same concepts from a Windows host. If we are conducting initial enumeration from a Windows laptop with no internet access, we are prevented from installing any extra tools that help us, the Windows Nmap version. In such limited scenario, we are forced to use the 'living off the land' strategy discussed earlier. Luckily, there are a few built-in PowerShell functions we can use.

The Test-NetConnection function checks if an IP responds to ICMP and whether a specified TCP port on the target host is open. For instance, for the Windows 11 client, we can verify if the SMB port 445 is open on a domain controller as follows.

```
PS:\Users\student> Test-NetConnection -Port 445 192.168.0.151
ComputerName        : 192.168.0.151
RemoteAddress       : 192.168.0.151
RemotePort          : 445
InterfaceAlias      : Ethernet0
SourceAddress       : 192.168.0.152
TcpTestSucceeded    : True
```

> Listing 71 - Port scanning SMB via PowerShell

The returned value in the TcpTestSucceeded parameter indicates that port 445 is open. We can further script the whole process in order to scan the first 1024 ports on the Domain Controller with the PowerShell-liner shown below. To do so we need to use a TcpClient Socket object as Test-NetConnection adds additional traffic that is not needed for our purposes.

```
PS:\Users\student> 1..1024 | % { (New-Object Net.Sockets.TcpClient).Connect("192.168.0.151", $_) | echo "TCP port $_ is open" 2>$null
TCP port 88 is open
```

> Listing 72 - Automating the PowerShell scanning

By piping the first 1024 integer into a for-loop which assigns the incremental value to the $_ .. Then, we create a Net.Sockets.TcpClient object and perform a TCP connection against the target IP on specific port, and if the connection is successful, it prompts a message that includes the open TCP port. We've covered the starting point of PowerShell's abilities, which can be further extended to match the traditional Nmap features.

## 6.3.4 SMB Enumeration

The security record of the Server Message Block (SMB) protocol has been poor for many years due to its complex implementation and operation. From unauthenticated SMB sessions in Windows 2000 and XP, to a plethora of SMB bugs and vulnerabilities over the years, SMB has had its fair share of action. this in mind, the SMB protocol has also been updated and improved in parallel with Windows releases. The NetBIOS listens on TCP port 139, as well as UDP ports. It should be noted that SMB (TCP port 445) and NetBIOS are two separate protocols. NetBIOS is an independent
