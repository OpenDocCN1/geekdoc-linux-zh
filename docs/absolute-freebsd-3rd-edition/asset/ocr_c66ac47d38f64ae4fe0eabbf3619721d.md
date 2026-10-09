first category listed is the directory where it appears in the Ports Collection. In this case, the port appears in the *archivers* directory.

We then have dependencies. B _deps lists the build dependencies—that is, other software that must be installed to build this port. R _deps lists runtime dependencies, software needed for this to actually run. This is a Perl module, so it needs a Perl interpreter. Some software must be extracted or decompressed by particular tools, specified in E _deps. The P _deps field lists any dependencies for patching the software—rare pieces of software must be patched with a certain tool. The F _deps field is similar, specifying *fetch dependencies*—that is, any special software that must be used to download the software.

Finally, the WWW space gives the home page of the software.

# # Searching the Index

The Ports Collection includes tools to search the index. If you want a particular program, you might be better off finding the ports directory with `pkg search` or even `locate -i`. Reserve searching the Ports Collection to answer questions like "What ports use SNMP?"

If you know the name of a piece of software, search INDEX for it with `make search`. Here, I look for ports with names that include *net - snmp*:

```
# cd /usr/ports
# make search name=net - snmp
Port:  	 net - snmp - 5.7.3_12
Path:  	 /usr/ports/net-mgmt/net - snmp
Info:  	 Extensible SNMP implementation
Maint: 	 zi@FreeBSD.org
B - deps: 	 perl5 - 5.24.1
R - deps: 	 perl5 - 5.24.1
WWW: 	 http://net - snmp.sourceforge.net/

Port: 	 p5 - Net - SNMP - 6.0.1_1		 p5 - Net - SNMP - 365 - 3.65
- S n i p -
```

As of this writing, FreeBSD has several ports with *net - snmp* in their name. The first is the current standard net - snmp software collection ❶. Others include Perl libraries that use SNMP over the network but otherwise have nothing to do with the net - snmp suite, old versions of