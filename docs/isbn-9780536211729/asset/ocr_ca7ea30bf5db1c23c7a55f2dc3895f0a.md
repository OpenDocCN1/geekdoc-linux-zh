# 8.19.1 Installing Tripwire

First, download the latest free version (or buy the commercial version). The free version may be downloaded from the following site after giving some contact information to Tripwire, Inc. Although this version has some restrictions, the company has released the Tripwire source for Linux under the GPL. It cannot be put on the CD-ROM or Web due to U.S. export restrictions and license restrictions. Note that you will be offered binaries only. They claim to support Red Hat only. It does not require RPM and should work on other distributions. You will want to operate in a newly created empty directory for this purpose, such as tripwire, after downloading from

www.tripwire.com/downloads/

The download will leave a gzipped tar file in your directory. Unzip it and extract it with the usual

```
gunzip Tripwire_221.tar.gz
tar -xovf Tripwire_221.tar
```

or

```
tar -xzovf Tripwire_221.tar.gz
```

As root, issue the command

```
./install.sh
```

It will check for needed programs on the system, such as tar, awk, and accept it. Then it will ask you to read the license and accept it Tripwire passphrases. They may be up to 1024 characters each. Tripwire does not reject easy-to-crack passwords. Pick good passwords that are hard to break, as discussed in "Passwords—A Key Point for Good Security" on page 35. You will be asked to re-enter your passphrases several times during configuration as it invokes various Tripwire programs that require the passphrases to ensure security. By default, it creates the Tripwire system under /usr/TSS. It will suggest that you inspect and remove the clear-text version of the Tripwire configuration file.

```
/usr/TSS/bin/twcfg.txt
```

It then suggests, abruptly, that you read the release notes and have a nice life. Policies are stored under /usr/TSS/policies. The twpol.txt file controls what files Tripwire will watch and what to expect from each. It is well commented, to understand what designated log files will grow, and understands what device files are. It is a good idea to spend some time editing this file at this point. The alternative is significant both later. Install the documentation with the following commands: