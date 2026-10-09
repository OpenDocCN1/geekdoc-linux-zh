The ifconfig tool found in `net_tools` has a defect and does not load the `ipv6.o` module automatically. If you have this problem, you may want to recompile the kernel’s `ipv6` as a non-module.

If you need to reconfigure the kernel, go to the source directory. (Some distributions do not automatically install the kernel source for some reason, so you may need to download and install it. The Web site [http://www.kernel.org](http://www.kernel.org) is a good source.) Be sure that all your settings are correct in all the options, and select Experimental Drivers. Next select IPv6 in the Network Settings menu. You can find it in the It Is Safe to Leave These Untouched section. Some kernel configurations permit you to select exclusive IPv6. Don't do it. Again, you may want to include the IPv6 in the kernel and *not* compile it as a module. That can save you some debugging time.

Be sure to keep a backup of your old kernel. If you have a problem, you can use it to get back to a sane state.

# ## Configuring the Tools

The next test needed is the tools. If you have confirmed kernel support, run ifconfig without any arguments. It displays the current configurations of each network interface. If it supports IPv6, the list includes an IPv6 address in the second or third line of each interface.

If you do not see the addresses, run it again with a `-help` option. The command then lists for you all the supported protocols. You probably won't see IPv6 in this case. If it’s omitted, you need to get the `net_tools` RPM and reconfigure it and compile it. After installation, configure it using `configure.sh` and enable IPv6. You can include IPv6 over IPv4, if you would like, but that may be unnecessary. Compile the package and copy all the executables to their typical homes (this is often `/sbin`).

Again, keeping a backup of your tools is a very good idea. (You may note that the default settings of `configure.sh` are the same as your old install. So if your backup does not work, you could simply recompile.)

After you compile and install your tools and kernel, reboot the host. When the system is ready again, running ifconfig shows you the mapped addresses for its assigned IPv4 address. You can even add an IPv6 alias with the following:

```
```
ifconfig eth0 add <IPv6 Address>
```
```

For example

```
```
ifconfig eth0 add 2FFF::80:453A:2348
```
```

After you have your system all set up, you can begin to write a few IPv6 programs.