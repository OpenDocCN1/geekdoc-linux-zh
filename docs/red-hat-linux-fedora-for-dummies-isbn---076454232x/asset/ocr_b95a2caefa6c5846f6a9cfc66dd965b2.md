# Chapter 19: Building a Streaming Audio Server

If your computer doesn’t have a DVD-ROM drive, you have to use the coupon in the back of this book to obtain Red Hat Linux on CD-ROMs. After you receive the CD-ROMs, use them to install the libxslt and automake packages.

Now you have to download the Iccast2 and lces2 software from the Internet.

+   3. **Connect your computer to the Internet.**
   The method you use to connect to the Internet depends on the kind of service you subscribe to. Refer to Chapters 5, 6, and 7 for information about how to connect your computer to the Internet.

+   4. **Enter this command in a GNOME Terminal window:**
   ```
   export CVSROOT=:pserver:anoncvs@xiph.org:/usr/local/cvsroot
   ```
   This command sets up an *environmental variable* that CVS needs in order to complete its download. Environmental variables tell the shell you’re working in — bash, in this case — where to find elements such as files and directories.

+   5. **Tell your CVS client to log in to the remote CVS server. Enter this command to log in to the remote system:**
   ```
   cvs login
   ```

+   6. **Enter anoncvs when you’re prompted for the CVS server password.**
   After you have logged in, you can download — or *check out* (co), in CVS parlance — the software. Enter the first of the following commands in order (wait for each one to finish before continuing to the next one.)

+   7. **After you’re logged in, you can download — check out (co), in CVS parlance — the software:**
   ```
   cvs co icecast
   cvs co ices
   cvs co libshout
   cvs co ogg
   ```
   You see the files displayed as they’re downloaded, and the CVS checkout process is complete.

The following set of steps describes how to configure, compile, and install your multimedia server:

+   1. **Run the command in a terminal emulator:**
   ```
   export LD_LIBRARY_PATH=/lib:/usr/lib:/usr/local/lib
   ```
   This environmental variable is needed so that the compiler knows where to find several libraries.