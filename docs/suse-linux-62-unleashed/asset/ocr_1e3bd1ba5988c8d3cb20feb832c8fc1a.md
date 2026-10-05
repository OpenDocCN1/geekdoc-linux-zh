# Networking and Internet Services
PART II

<dir> is the server directory that is checked whenever clients use the cd command. For security reasons, specify directories relative to the FTP home directory for your anonymous users. An example of the cdpath command follows:

cdpath/pub/music
cdpath/pub/coffee

If clients type the command cd instant, the server examines the directories in the following order:

+   1. ./instant
2. Aliases called instant (For more information, see the description of alias earlier in this chapter.)
3. /pub/music/instant
4. /pub/coffee/instant

compress
-ftpd (the FTP server I have currently installed) offers a special compress feature that enables the server to compress or decompress a file before transmission. With this capability, a client who might not have the necessary software to decompress a file can still fetch it in a usable form. For example, a file on your server is compressed using gzip, and a Windows client needs to get it out but does not have the DOS version of gzip available.

The compress command's format follows:

compress <switch> <classglob>

<switch> is either YES (to turn on this feature) or NO (to turn it off). <classglob> is a comma-separated list of classes to which this compress option applies.
There is, of course, a cache to using this command. You need to configure the ftpconversions file so the server knows which programs to use for certain file extensions.
The default configuration supports compression by either /bin/compress or /bin/gzip.

For more information, see the section titled "Converting Files On-the-Fly—The ftpconversions File" later in this chapter.

# tar

Almost identical to the compress option, tar specifies whether the server will tar and untar files for a client on demand. The format of this command follows:

tar <switch> <classglob>