```
```
root@kali-2019: /usr/share/metasploit-framework/modules# cd exploits
root@kali-2019:/usr/share/metasploit-framework/modules/exploits# ls -l
total 80
drwxr-xr-x 3 root root 4096 Jul 11 09:31 aix
drwxr-xr-x 6 root root 4096 Jun 19 15:14 android
drwxr-xr-x 5 root root 4096 Jun 19 15:14 apple_ios
drwxr-xr-x 3 root root 4096 Jun 19 15:14 bsdi
drwxr-xr-x 3 root root 4096 Jun 19 15:14 dialup
-rw-r--r-- 1 root root 2698 Jul 2 15:55 example.rb
drwxr-xr-x 3 root root 4096 Jun 19 15:14 firefox
drwxr-xr-x 9 root root 4096 Jun 19 15:14 freebsd
drwxr-xr-x 3 root root 4096 Jun 19 15:14 hpx
drwxr-xr-x 21 root root 4096 Jun 19 15:14 linux
drwxr-xr-x 3 root root 4096 Jun 19 15:14 mainframe
drwxr-xr-x 26 root root 4096 Jul 11 09:31 multi
drwxr-xr-x 4 root root 4096 Jun 19 15:14 netware
drwxr-xr-x 13 root root 4096 Jun 19 15:14 osx
drwxr-xr-x 4 root root 4096 Jun 19 15:14 qnx
drwxr-xr-x 8 root root 4096 Jun 19 15:14 solaris
drwxr-xr-x 14 root root 4096 Jul 11 09:31 unix
drwxr-xr-x 51 root root 4096 Jul 11 09:30 windows
```
```

As you can see, within the modules are the seven types of modules we saw earlier. We can delve even deeper by changing directories to the exploits subdirectory and next the windows subdirectory.

```
```
kali > cd exploits kali > ls -l
```
```

Now we can see that the exploits categorized into directories for a particular platform (in general, platform is equivalent to operating system with a few exceptions such firefox, netware and a few others).

If we were looking to exploit a windows system, we would want a Windows exploit, so let’s navigate to that sub-
directory.

```
```
kali > cd windows kali > ls -l
```
```