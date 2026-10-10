```
# tail /var/log/dpkg.log

2016-12-22 09:04:05 status installed kali-linux-gpu:amd64 2016.3.2
2016-12-22 09:20:07 startup packages remove
2016-12-22 09:20:07 status installed kali-linux-gpu:amd64 2016.3.2
2016-12-22 09:20:07 remove kali-linux-gpu:amd64 2016.3.2 <none>
2016-12-22 09:20:07 status half-configured kali-linux-gpu:amd64 2016.3.2
2016-12-22 09:20:07 status half-installed kali-linux-gpu:amd64 2016.3.2
2016-12-22 09:20:07 status config-files kali-linux-gpu:amd64 2016.3.2
2016-12-22 09:20:07 status config-files kali-linux-gpu:amd64 2016.3.2
2016-12-22 09:20:07 status config-files kali-linux-gpu:amd64 2016.3.2
2016-12-22 09:20:07 status not-installed kali-linux-gpu:amd64 <none>
```

# Reinstalling Packages with apt --reinstall and aptitude reinstall

When you mistakenly damage your system by removing or modifying certain files, the easiest way to restore them is to reinstall the affected package. Unfortunately, the packaging system finds that the package is already installed and politely refuses to reinstall it. To avoid this, use the --reinstall option of the apt and apt-get commands. The following command reinstalls postfix even if it is already present:

```
# apt --reinstall install postfix
```

The aptitude command line is slightly different but achieves the same result with aptitude reinstall postfix. The dpkg command does not prevent re-installation, but it is rarely called directly.

| Do Not Use apt --reinstall to Recover from an Attack | Using apt --reinstall to restore packages modified during an attack will certainly not recover the system as it was. |
| After an attack, you can't rely on anything: dpkg and apt might have been replaced by malicious programs, not reInstalling the files as you would like them to. The attacker might also have altered or created files outside the control of dpkg. |

Remember that you can specify a specific distribution with apt as well, which means you can roll back to an older version of a package (if for instance you know that it works well), provided that it is still available in one of the sources referenced by the sources.list file:

```
# apt install w3af/kali-rolling
```

# Leveraging --force-* to Repair Broken Dependencies

If you are not careful, the use of a --force-* option or some other malfunction can lead to a system where the APT family of commands will refuse to function. In effect, some of these options allow