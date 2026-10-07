user commits a file back to the CVS repository. CVS merges the changes automatically unless there is an obvious conflict, in which case CVS reports it to the user to fix.

# The Client/Server Model

The other major difference, and it's a biggie, between RCS and CVS is that CVS operates on a client and server model and is designed to work across networks rather than just on the local machine. This makes life much easier for people who are all working in separate locations, at least in terms of committing and retrieving the latest versions of files. Don't think, you are unable to use CVS on a single machine with multiple users. Your server and your clients may be located physically on the same hardware.

# Installing CVS

If CVS is not already installed on your system, you can grab the source or binaries from the CVShome.org Web site at http://www.cvhome.org/. To find out whether CVS is already on your system, type cvs --version and you will see output as shown in Figure 7.7 if CVS is already installed.

![](bbox=[0.19, 0.545, 0.693, 0.893])