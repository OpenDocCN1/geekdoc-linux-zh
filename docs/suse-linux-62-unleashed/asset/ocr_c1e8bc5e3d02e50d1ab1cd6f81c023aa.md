# Caution

Do not attempt the following bdflush berm tweaks without first consulting and understanding the contents of file sysctl/vm.txt in the kernel source Documentation directory . Each of the values are explained in that document. If the file does not exist, the linux RPM. It will have a name similar to linux-2.2.10-3.1386.rpm.

The following two commands will change how Linux manages memory. They are not likely to make too much of a performance difference except in situations where your server is used to access large files by many users simultaneously.

```
echo '00 58 64 64 6000' > /proc/sys/vm/bdflush
echo '00 68 08' > /proc/sys/vm/bdffem
```

Some other possible enhancement techniques include faster network hardware and wiring, a better server hard disk, more server memory, or a server CPU upgrade. If you want to improve performance, it's important to begin identifying the component that is limiting performance, also known as the bottleneck. The best way to do this is to perform measurements of disk activity, network traffic, memory usage, and CPU load. After this is done, the bottleneck can normally be easily identified and dealt with.

If measurement data does not point to a clear culprit, try using this technique. One of the best bottleneck analysis techniques is to deliberately decrease the performance of a suspected bottleneck. If system performance suffers by a similar proportion, you've found a bottleneck. If system performance suffers only slightly, continue looking.

# Testing Your Configuration

After creating the configuration file, you should test it for correctness. Start by making the client and server can ping each others' IP address. Without a functioning network, Samba will not work.

Next use the testprogram. This is a simple test to check the /etc/smb.conf configuration file for internal correctness. If this program reports no problems, you can use the configuration file with confidence that smbd will successfully load the configuration file.