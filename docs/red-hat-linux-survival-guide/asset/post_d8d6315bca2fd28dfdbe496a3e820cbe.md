
```
# For the primary server
ftpd@206.171.50.50 : ALL : twist exec \
/usr/sbin/in.ftpd -l -a /etc/ftp/ftpaccess
```
```
# For the virtual FTP server
ftpd@206.171.50.51 : ALL : twist exec \
/usr/sbin/in.ftpd -l -a /etc/ftp/client1.ftpaccess
```
```
# For the second virtual FTP server
ftpd@206.171.50.52 : ALL : twist exec \
/usr/sbin/in.ftpd -l -a /etc/ftp/client2.ftpaccess
```

- 5. Now create the /etc/ftp directory and move the /etc/ftpaccess file into that directory.
- 6. Make two copies of the /etc/ftp/ftpaccess file such that you have /etc/ftp/client1.ftpaccess and /etc/ftp/client2.ftpaccess files.
- 7. Remove any virtual keywords from the /etc/ftp/ftpaccess file used for the mail FTP server.
- 8. Modify the client1.ftpaccess file so that it has a line such as the following:
  virtual 206.171.50.51 root /home/client1/ftp
- 9. Similarly, modify the client2.ftpaccess file to have a line such as:
  virtual 206.171.50.52 root /home/client2/ftp
  Don't forget to replace the IP addresses and the directory path with your own.
- 10. Now copy the anonftp files in the /home/client1/ftp and /home/client2/ftp directories.
- 11. Restart the xinetd server using the following command:
  killall -USR1 xinetd
  That's all there is to it! Now you have two virtual FTP sites that can be accessed via their respective host names or IP addresses.

## Monitoring transfer log

Logging is very important for FTP service because you want to know who is doing what with your files. The wu-ftpd server logs transfers in the xferlog file, which typically resides in the /var/log directory. You can customize logging using the log commands and log transfers keywords discussed earlier.

If you are interested in monitoring xferlog on a regular basis, you can try Dump xfer. You can download this package from the following FTP address:

```
ftp://ftp.microimages.com/tools/dump_xfer.1.2.tar.gz
```

## Becoming an Efficient FTP User

In this section I show you how to use FTP service effectively to download or upload files to and from FTP servers.

## Using command-line FTP client

Virtually all modern operating systems have a command-line FTP client available by default. Yes, even the newer Windows (98 or more recent) have a built-in command-line FTP client. Interestingly, almost all the FTP clients on various popular operating systems behave pretty much in the same fashion. So, if you know how to use the Linux FTP client, you should be able to use it under Windows or even Mac OS X (which is based on FreeBSD).

## Connecting to a FTP server

To FTP to a site called ftp.domain.com from any machine with a command-line FTP client run ftp ftp.domain.com command from the Linux shell or xterm window under the X Window System, or the equivalent. For example, run this command from the DOS shell window under Windows.

After you’ve run this command from a shell window, the FTP client attempts to connect to the FTP site. Once you’re connected you’ll be presented with username and password prompts. Enter the appropriate username and password. If you want to access the remote FTP site as an anonymous user, you can enter anonymous or ftp as the username and then enter your e-mail address as the password.

## Navigating the FTP site

After you are logged in, you can navigate directories using the cd command and view directory listing using dir or ls command. Any time you wish to know what directory you are currently browsing you can enter the pwd command to view the directory path.

## Setting the transfer mode

By default, most FTP clients set the transfer mode to binary, which should work for all situations. If you do not see a message during your session about the transfer mode, you can set it to binary by entering bin or binary as the command. If for some reason you need to switch to text mode transfer, you can enter text to change to text mode.

## Downloading files and directories

To download a file from the site you can enter get filename command. The file will be downloaded to the current directory of your local system. To get multiple files from a directory you can use the mget filename1 filename2 filename3 [filenameN] command.

You can also use wild cards such as mget *.file_extension to download files with a specific extension. For example, mget *.gif *.jpeg allows you to download all GIF and JPEG files in the current directory of the local system from the current directory of the remote FTP site.

When using the mget command you will notice that the FTP client will prompt you before each file is downloaded. If you wish to have it download these files without asking you for each one, simply use the prompt command to toggle the prompt mode and then run the mget command. Also, if you wish to see a visual indication of files being downloaded you can enter hash command to toggle displaying of # character as download progresses.

![](img/9eb7e89292d2f85707b4d49102c865b7_456_0.png)

> For very large downloads displaying # is useless because you will have many screens full of them.

If you are downloading files from a Linux FTP server to a Linux FTP client system you can take advantage of a special feature that is often also found in other Unix-based FTP servers that allows you to download an entire directory by specifying the get directory_name command. You can even compress the transfer, which speeds up the download. For example to download a directory called pub in compress mode you can enter get pub.gz command. Note that such commands only work if the FTP server permits this operation.

## Restarting a failed download

If your download session fails due to a system or network problem you can restart the download by issuing a reget filename command after you have logged on to the FTP server again. This is a great technique for recovering failed download transfers of large files. For example, if you have downloaded 10MB of a 30MB file and got interrupted due to a network problem or system error, you can connect back to the FTP server again and issue the reget command for the same filename. This will save you time and reduce bandwidth waste.

## Uploading files

The precondition for uploading a file is to have the appropriate permissions to upload into a FTP server. Never upload files to someone else's FTP server without permission; this can be considered as a serious criminal activity.

Assuming that you have permission to upload files on to the FTP server you are connected to, run the put filename command to upload the named file from your local system's current directory. If the file is in a different directory you can change your local system's current directory using the lcd command. For example, if you started the FTP client from the /tmp directory and want to upload a file from the /root/myfiles directory after you are at the FTP client prompt, you can run lcd /root/myfiles to set the local system's current directory to /root/myfiles. Then you can run the put command to upload a file.

If you wish to upload multiple files you can run mput filename1 filename2 ... [filenameN] command, or you can use wildcards such as mput *.file_extension to upload files of certain extension.

If you have permission to create/delete directories in the FTP site, you can use mkdir directory and rmdir directory commands to do so respectively. Also, if you wish to rename a file on the server use the rename filename command.

## Escaping to your current shell

When you are connected to a FTP site you can still escape temporarily to your current shell window by entering ! at the FTP command prompt. You can return to your FTP session by entering exit command at the shell prompt.

## Aborting file transfer

After you have started upload or download transfer you can abort it by pressing the Ctrl+C key sequence for a few seconds. Upload transfer is aborted immediately; download transfers might take a few seconds or more.

## Closing FTP connection

After you have completed your upload or download tasks, you can simply terminate the FTP connection by entering quit command.

## Using .netrc to automate FTP sessions

If you perform routine download or upload tasks from one or more FTP sites you can save yourself some typing by creating a .netrc file in your home directory. The Linux FTP client automatically reads this file for a matching record for the host name it is currently connecting to. For example, Listing 14-3 shows a sample .netrc file for a host name called ftp.domain.com.

### Listing 14-3 An example .netrc file

```
machine ftp.domain.com
login your_username
password your_password
macdef init
bin
prompt
cd /some/path
get filename
quit
```

Whenever you connect to ftp.domain.com this sample .netrc file will be read from your home directory (i.e., ~/.netrc) and the FTP client
