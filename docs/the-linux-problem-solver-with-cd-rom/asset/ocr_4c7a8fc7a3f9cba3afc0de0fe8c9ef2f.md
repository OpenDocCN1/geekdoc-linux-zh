# younger

If a file you're distributing has a newer modification date on the remote host, this command makes sure that you don't touch the file on the remote host. This is particularly useful for debugging purposes when combined with the verify dist option, because it tells you what files have been customized on a remote host, then leaves them untouched.

# nodescend

Don't go into subdirectories and examine their contents.

# nochkwoner, nochkgroup, nochkmode

Ignore owner, group, and mode (permission) differences, respectively.

# follow

Resolve symbolic links and treat them as if they were real files or directories.

# Using ssh with rdist

Since rsh isn't very secure, many systems administrators opt to turn it off. If they do use it, they don't allow root access through it. It is, however, possible to configure ssh to perform the same thing as rsh, through either configuration or authorized keys. (For more information on ssh, consult Chapter 2.) The process is different for ssh versions 1 and 2, so we'll first go over version 1 and then talk about the next version.

# PROBLEM 29

> **Symptoms:** Accidental transfer of large amounts of data. rdist gets into infinite loops, filling up the disk.
> 
> **Problem:** follow is a dangerous dist option.
> 
> **Fix:** Only use follow when you're absolutely sure what it is you intend to copy—such as a single directory. You can, however, use nodescend in combination with follow to get a flat directory free of symbolic links. Because rdist will only install the first level of directories it sees when given the nodescend dist option, your Distfile needs to reflect all files in a directory (here, for a directory dir):
> 
> ( dir/* ) -> ( machines )
> 
> install -ofollow,nodescend ;