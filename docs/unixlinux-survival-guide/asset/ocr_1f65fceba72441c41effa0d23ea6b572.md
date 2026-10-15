```
# clean up afterwards
@args_rm = ('rm', '-r', "$the_dir");
system(@args_rm) == 0
    or die "$0: couldn't remove the dir: $!";

# EOF
```

One word of warning first: this script is able to seriously destabilize a system. Use it at your own risk. It works on every Solaris, BSD, or OS X system. It uses the mkfile command that is part of the indicated systems. The original use of this command is to create swap files in the filesystem. The size unit is specified as b = blocks, k = kilobyte, m = megabyte, or g = gigabyte. The script creates a directory by using the path and filename supplied with the -d option. The size is supplied with the -s option, and the file will be copied -n times within the directory.

To use the script on HP-UX, you have to replace mkfile with prealloc. This command does not know about the options mkfile understands, though. It accepts a filename and a number (interpreted as bytes). Another solution would be the use of a tar archive of the /usr/local tree, for example, and to use this tar archive as a file to be copied.

Next, take a look at Listing 5.25.

# LISTING 5.25 Using loadtest.pl

```
erikk@unixhost> ./loadtest.pl -d tests/ltest1 -s 2m -n 50
```

The command in Listing 5.25 initiates the following events: It creates a file in /tests/test1 with a size of 2 megabytes. The file would be copied 50 times. Then the script removes the created files and directories again. The script will not check if there is sufficient room for the actions to be performed; if it is out of disk space, it terminates with an error message and without cleaning up. To create a usable load situation, you have to make sure that the disk or array to be tested gets filled close to capacity. The script can be used to test disks and network connections. To test a network connection, you should simply use a directory mounted via NFS. You should never use the script to test a network connection inside a production network, though. Listing 5.26 gives an example.

# LISTING 5.26 Using loadtest.pl over a Network.

```
erikk@unixhost> mount linuxhost:/data1/tests /myount/test
erikk@unixhost> ./loadtest.pl -d /myount/test/ltest1 -s 2m -n 50
```