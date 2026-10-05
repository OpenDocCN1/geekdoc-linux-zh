# CHAPTER 9 • ADVANCED VIRTUAL MACHINE FEATURES

This utility supports a /format parameter to retrieve WMI information in CSV format. For example, take a look at that CD-ROM drive again at VM001:

```
wmic path Win32_CDROMDrive get "Caption,Drive,Manufacturer" / 
format:csv
```

Node, Caption, Drive, Manufacturer
VM001, NECVMVar VMware SATA CD00,Z; (Standard CD-ROM drives)

Notice that a get parameter was used to retrieve only specified properties. To retrieve all properties, provide the get parameter without any properties. Combine this new technique with the Invoke-VMScript cmdlet:

```
$script = "wmic path Win32_CDROMDrive get /format:csv"
$Output = Invoke-VMScript $script -VM VM001 
-HostCredential $HostCredential -GuestCredential $GuestCred 
-ScriptType "bat"
```

At this point PowerShell has the CSV-formatted output as plain text, some stored in the $Output.ScriptOutput property. With a quick trip through the ConvertFrom-Csv command, that plain text can be converted into a useful object:

```
$cdrom = $Output.ScriptOutput.Trim() | ConvertFrom-Csv
```

Whenever you are forced to work with text, some additional manipulation may be necessary. In this case, the .Trim() method was used to strip off the empty line returned by wmic at the start of the output; without it, the CSV would be invalid. CSV headers must start at the first line in a CSV file. The $cdrom variable now contains the desired information in a nice PowerShell object-oriented way:

```
$cdrom
Node : VM001
Availability : 3
Capabilities : {3;7}
CapabilityDescriptions : {Random Access; Supports Removable Media}
Wait, wait, checking text again...
CapabilityDescriptions : {Random Access; Supports Removable nMedia}
Caption : NECVMVar VMware SATA CD00
CompressionMethod : Unknown
ConfigManagerErrorCode : 0
ConfigManagerUserConfig : FALSE
CreationClassName : Win32_CDROMDrive
DefaultBlockSize :
```