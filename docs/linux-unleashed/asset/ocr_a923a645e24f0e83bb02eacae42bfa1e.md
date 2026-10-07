A better way to handle the load on your system is to use the MaxConnections keyword, which sets the number of clients you support concurrently. You have to experiment to determine the best balance between system load and user service. A good starting point for a fast Linux system (80486 or Pentium CPU) is 15 to 25 users. If you are going to run a Web server at the same time, you may want to cut down this number a little, though, to spare system resources. This variable is set like this:

```
MaxConnections: 15
```

If the number of users is exceeded, an error message is generated when the connection is attempted. You can set a number of file decoders for your system. This is used when a user requests a file from Gopher and adds an extension (such as .Z, .gz, or .zip) for a compression or archive utility. The decoders recognize the extension the user supplies and invoke the proper utility to send the file properly decoded. Most gopherd.conf files have the following decoder lines already in the setup:

```
```text
decoder: .Z /usr/ucb/zcat
decoder: .gz /usr/gnu/bin/zcat
#decoder: .adpcm /usr/openwin/bin/adpcm_dec
#decoder: .z /usr/gnu/bin/zcat
```
```

The last two decoders are commented out and can be uncommented if you want to offer files in these formats through Gopher. You can also add other extensions by adding new lines with the binary name (and its full path).

In addition, the amount of time a cache file stays valid should be set. This is controlled by the line using the keyword Cachetime. Set this value to a reasonable value, such as 180 seconds. You should have a line that looks like this in the gopherd.conf file:

```
Cachetime: 180
```

You can use the gopherd.conf file to restrict access to some files on your system by using the ignore keyword. Usually the gopherd.conf file has a number of defined ignores, such as these:

```
```text
ignore: lib
ignore: bin
ignore: etc
ignore: dev
```
```

Any file with this type of extension is ignored. If there is a particular file extension you want to protect, add it to the list. For example, if your accounting system uses the extension .acct, you can have the Gopher clients ignore all these files by adding this line:

```
ignore: acct
```