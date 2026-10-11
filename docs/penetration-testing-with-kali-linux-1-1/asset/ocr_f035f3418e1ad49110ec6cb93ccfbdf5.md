![](bbox=[0.125, 0.04, 0.285, 0.1])

We can discover the hostname with the aptly-named **hostname**⁴⁴⁴⁴⁵ command, which is installed on both Windows and Linux.

Let's run it on Windows first,

```
```
C:\Users\student>hostname
client251
```
```

*Listing 518 – Getting information about hostname on Windows*

and then on Linux:

```
```
student@debian:~$ hostname
debian
```
```

*Listing 519 – Getting information about hostname on Linux*

The fairly generic name of the Windows machine does point to a possible naming convention within the network that could help us find additional workstations, while the hostname of the Linux client provides us with information about the OS in use (Debian).

Identifying the role of a machine can help us focus our information gathering efforts.

# 18.1.1.3 Enumerating the Operating System Version and Architecture

At some point during the privilege escalation process, we may need to rely on *kernel*⁴⁴⁶ exploits that specifically exploit vulnerabilities in the core of a target's operating system. These types of exploits are built for a very specific type of target, specified by a particular operating system and version combination. Since attacking a target with a mismatched kernel exploit can lead to system instability (causing loss of access and likely alerting system administrators), we must gather precise information about the target.

On the Windows operating system, we can gather specific operating system and architecture information with the **systeminfo**⁴⁴⁷ utility.

We can also use **findstr**⁴⁴⁸ along with a few useful flags to filter the output. Specifically, we can match patterns at the beginning of a line with **/B** and specify a particular search string with **/C:**.

In the example below we'll use these flags to extract the name of the operating system (Name) as well as its version (Version) and architecture (System).

```
```
C:\Users\student>systeminfo  |  findstr /B /C:"OS Name" /C:"OS Version" /C:"System Type"
    Microsoft Windows 10 Pro
    10.0.16299 N/A Build 16299
    X86-based PC
```
```

*Listing 520 – Getting the version and architecture of the running operating system*

+   ⁴⁴⁴ (Microsoft, 2017). https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/hostname
+   ⁴⁴⁵ (Peter Tobias, 2003). https://linux.die.net/man/1/hostname
+   ⁴⁴⁶ (Wikipedia, 2019). https://en.wikipedia.org/wiki/Kernel_(operating_system)
+   ⁴⁴⁷ (Microsoft, 2017). https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/systeminfo
+   ⁴⁴⁸ (Microsoft, 2017). https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/findstr