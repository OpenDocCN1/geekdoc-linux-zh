+   L indicates that the file is improperly a symbolic link.
U indicates that the file has the wrong user ID (UID) assigned.
G indicates that the file has the wrong group ID (GID) assigned.
T indicates that the file has the wrong file creation time.
C indicates that the file is a configuration file that is expected to change.

In the previous example, two files have the wrong checksum and the wrong creation date, and they are the wrong size. These are all things you would expect because these are not the original files. The file that were installed over the original files. The file that is missing is the S80sendmail script we deleted in Listing 3.3. All of the other files associated with the Sendmail RPM check out. But even these three errors might set off alarm bells with the system's computer security officer. For this reason, clean out the RPM installation before installing Sendmail from source code as described in the following section.

# Downloading and Compiling Sendmail

Even if your Linux system comes with its own version of Sendmail, obtaining the latest Sendmail source code distribution provides useful documentation, tools, and sample configuration. Additionally, there are times when you need a security fix or update and the latest version of Sendmail has not yet been posted as an RPM or other binary distribution.

The latest Sendmail distribution is available via anonymous FTP from ftp.sendmail.org, where it is stored in the pub/sendmail directory. When you change to that directory, an informational message is displayed that tells you about the latest version of Sendmail. New releases are constantly being created. The following examples are based on Sendmail V8.11.0.

> NOTE Remember that things will change for future releases, so always review the readme files and installation documents that come with new software before beginning an installation.

To compile the Sendmail program, download the compressed tar file as a binary file and then uncompress and extract it with the tar command, as shown in Listing 3.10.

Listing 3.10 Downloading the Sendmail Source Code

```
[craig]$ ftp ftp.sendmail.org
Connected to ftp.sendmail.org.
```