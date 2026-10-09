CGIWrap is distributed as a gzip-compressed tar file. You decompress it by using `gzip` and extract it by using the `tar` utility.

Run the `Configure` script, which prompts you to answer many questions. Most of these questions are self-explanatory. Also note that there is a feature in this wrapper that differs from suEXEC. It enables you to create allow and deny files that can be used to restrict access to your CGI scripts. Both of these files have the same format, as shown in the following:

```
User ID
mailto:Username@subnet1/mask1,subnet2/mask2...
```

You can either have a single username (nonnumeric UID) or a user `mailto:ID@subnet/mask` line where one or more subnet/mask pairs can be defined. For example, if the following line is found in the allow file (you specify the filename).

```
mailto:kabir@192.168.1.0/255.255.255.0
```

user kabir's CGI scripts are permitted to be run by hosts that belong in the 192.168.1.0 network with netmask 255.255.255.0.

After you run the `Configure` script, you must run the `make` utility to create the CGIWrap executable.

To use the wrapper application, copy the CGIWrap executable to the user's `cgi-bin` directory. This directory must match the directory that you specified in the configuration process. The simplest way to get things going is to keep the `-username/public_html/cgi-bin` type of directory structure for the CGI script directory.

After you copy the CGIWrap executable, change the ownership and permission bits as follows:

```
chown root CGIWrap
chmod 4755 CGIWrap
```

Create three hard links or symbolic links called `nph-cgiwrap`, `nph-cgiwrapd`, and `cgiwrapd` to CGIWrap in the `cgi-bin` directory as follows:

```
ln [-s] CGIWrap cgiwrapd
ln [-s] CGIWrap nph-cgiwrap
ln [-s] CGIWrap nph-cgiwrapd
```