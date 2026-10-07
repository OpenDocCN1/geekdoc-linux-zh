If you have a gzipped, compressed, or tarred file you need to extract, the HylaFAX dumps contents from it into a temporary directory. For example, if you have the HylaFAX archive HylaFax-v4.0-tar.gz, you would unpack it and place it in a fax directory with these commands:

```
```
mkdir /usr/fax
cd /usr/fax
cp /tmp/HylaFax-v4.0-tar.gz .
gunzip HylaFax-v4.0-tar.gz
tar -xf HylaFax-v4.0-tar
```
```

Perform all these steps as root. Of course, you must substitute the directory in which you placed the HylaFAX archive for /tmp in the above commands. If you don't want to use /usr/fax as the HylaFAX directory, change those commands to your target directory, too.

# ## Compiling HylaFAX

After all the files are extracted in your fax directory, you need to invoke the C++ compiler to produce an executable. There may be some important information in a file in the subdirectory /port/linux, usually as a file called README. To compile HylaFAX, issue the following commands (remember you must be logged in as root):

```
```
configure
make clean
make install
```
```

There are a bunch of steps that appear from the configure and make commands that we'll look at in a moment. When you issue the configure command, you'll see a bunch of messages about which directories HylaFAX should use:

+   HylaFAX configuration parameters are:

Directory for applications:  /usr/local/bin
Directory for lib data files:  /usr/local/lib/fax
Directory for lib executables:  /usr/local/lib/fax
Directory for servers:  /usr/local/etc
Directory for manual pages:  /usr/local/man
Directory for documentation:  /usr/local/doc/HylaFAX
Directory for spooling:  /usr/spool/fax
Type of uucp lock files:  ascii
Directory for uucp lock files:  /usr/spool/uucp
Mode for uucp lock files:  0444
Type of PostScript imager:  gs
PostScript imager program:  /usr/local/bin/gs
Default page size:  North American Letter