# 1. Use ports, netstat, or lsof to see what ports have processes listening on them

This is an easy way to determine what services are running due to their well-known ports. The services associated with each commonly used TCP and UDP port are listed in Appendix C.

The best way to invoke netstat for this purpose is.

```
netstat -atuvp | more
```

The -a flag indicates that ports that are not connected to an associated port on another system should be listed. This is important in order to list servers that do not have clients presently. The -t and -u flags specify that only TCP and UDP services should be listed. The -v flag adds verbosity. The -p flag says to list the name of the active program using each port; it requires root permission.

I wrote the program to provide results in a form that is easier to interpret than netstat. Additionally, it flags suspicious ports that include active ports known to be used as popular cracker tools. Also, it flags high-numbered ports that are being used for daemons. Normally high-numbered ports are used by clients. These flagged ports too may be Trojan horses planted by crackers. Typical invocation is shown here.

```
ports | more
```

In this phase, we are concerned primarily with securing a system, and are not expecting to find that it has been compromised already. Some systems will be compromised already and some readers will be surprised. (Those who are surprised are asked to send me e-mail at book@verysecurelinux.com with the details.)

# 2. Examine the startup scripts

These will show those services that are supported via daemons. In distributions that follow the UNIX V-style of startup scripts, there are directories of the form /etc/rc.d/rc[0-6].d The normal running state is 3. This may be verified with the command

```
grep initdefault /etc/inittab
```

The output will look something this

```
id:3:initdefault:
```

Inspect this output to see what state number is listed, "3" in this case. Then issue the command

```
ls -F /etc/rc.d/rc3.d/S*
```