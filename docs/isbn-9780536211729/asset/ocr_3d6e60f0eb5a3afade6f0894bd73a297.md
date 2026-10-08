Installation of both libpcap and TCPDump is fairly straightforward as far as compiling software goes. Unarchive each piece of source code, run the configure script, compile, and install.

In essence:

```
tar -zxvf libpcap-<version>.tar.gz
cd libpcap-<version>
./configure
make
make install
```

Do the same for TCPDump:

```
tar -zxvf tcpdump-<version>.tar.gz
cd tcpdump-<version>
./configure
make
make install
```

Should you encounter problems while compiling the software, refer to previous chapters where the compile process is detailed further or, as an even better solution, practice your analyst skills by troubleshooting the error on the Internet. Chances are that someone else has encountered and solved the problem that you're working through.

# ## 11.2.2 TCPDump Options

TCPDump accepts a wide range of command-line options that alter its behavior, the amount of data captured, and the way in which the data is captured. Such a wide range of options means that you have the power to significantly change how the program operates. For TCPDump, you'll find that you frequently use a common set of options for most data capture activities, and you may not use others at all.

Some of the more commonly used options include those listed in Table 11.1.

**Table 11.1** Some Common Options for TCPDump

| **Option** | **Description** |
| :--- | :--- |
| `-i <interface>` | Specifies the interface to use. |
| `-v` | Produces output in verbose mode. |
| `-vv` | Produces output in really verbose mode. |
| `-x` | Causes TCPDump to print the packet itself in hexadecimal format. |
| `-X` | Causes TCPDump to also print the output in ASCII. |
| `-n` | Tells TCPDump not to perform DNS lookups for the IP addresses seen during the capture. |
| `-F <file>` | Reads the expression from <file>. |
| `-D` | Prints available interfaces. |
| `-s <length>` | Sets the length for each packet of the capture to <length>. |