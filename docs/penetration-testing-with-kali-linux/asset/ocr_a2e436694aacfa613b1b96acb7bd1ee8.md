It's best to combine atomic and manual enumeration techniques when assessing Active Directory. Even though we could theoretically gather the same information with a manual approach, graphical relationships often reveal otherwise unnoticed attack paths.

Let's get SharpHound up running.

SharpHound is available in few different formats: We can compile ourselves, use an already compiled executable, or use it as a PowerShell script. In our case, we use the PowerShell script that is located in C:\Tools\Client75. First, let's open a PowerShell window and import the script to memory:

```
PS C:\Tools> Import-Module \.SharpHound.ps1
```

Listing 785 - Importing the SharpHound script to memory

With SharpHound imported, we can now start collecting domain data. However, in order to run SharpHound, we must first run Invoke-BloodHound. This is not intuitive if we're only running SharpHound at this stage. Let's Get-Help to learn more about this command.

```
PS C:\Tools> Get-Help Invoke-BloodHound
```

# NAME

Invoke-BloodHound

SYNOPSIS
Runs the BloodHound C Ingestor using reflection. The assembly is stored in the file.

SYNTAX

Invoke-BloodHound [-CollectionMethod <String>] [-Domain <String>] [-SearchForest <String>] [-LdapFilter <String>] [-DistinguishedName <String>] [-ComputerFile <String>] [-OutputDirectory <String>] [-OutputPrefix <String>] [-CacheName <String>] [-Memcache <String>] [-NoZip] [-ZipPassword <String>] [-RebuildCache] [-RandomFilenames] [-ZipFilename <String>] [-LdapUsername <String>] [-TrackComputers] [-PrePrint] [-Strings <String>] [-DomainController <String>] [-LdapPort <Int32>] [-Secure [-DisableCertificateVerification] [-SkipPortCheck] [-PortTimeout <Int32>] [-SkipPasswordCheck] [-ExcludeDECs] [-Throttle <Int32>] [-Jitter <Int32>] [-Threads <Int32>] [-SkipRegistryLogged] [-OverrideUsername <String>] [-RealDNSName <String>] [-CollectAllProperties] [-Loop] [-LoopDuration <String>] [-LoopInterval <String>] [-StatusInterval <Int32>] [-Verbosity <Int32>] [-Help] [-CommonParameters]]

# DESCRIPTION

Using reflection and assembly.load, the compiled BloodHound C ingestor into memory and run it without touching disk. Parameters are converted to the equivalent CLI arguments

For the SharpHound executable and passed in via reflection. The appropriate function