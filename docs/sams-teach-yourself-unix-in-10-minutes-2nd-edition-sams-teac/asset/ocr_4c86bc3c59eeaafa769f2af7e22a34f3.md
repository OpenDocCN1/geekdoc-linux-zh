# Networking and Security 207

*.rpm packages? The tar files? All of these things can be sent to other Unix systems where other people can work with them or use them if needed.

The ftp command provides you with a way to retrieve files from remote machines that aren't set up to share file systems with yours. If your machine is running an FTP server, you might be able to use it to provide your files to the rest of the world as well. Contact your system administrator about this. Remember, this book covers only the use of Unix, so anything that needs to be added to your Unix system must be requested.

To use the ftp, simply enter the command as follows: ftp <ftp server>, where the FTP server is the IP address or hostname of a machine running an FTP server. If you've connected properly, you'll get a prompt for your credentials, which are your username and password. It should also be noted that FTP has the same inherent problems as telnet; the information is sent in clear text.

Some FTP servers enable you to connect without an account on the system. For these, use the username anonymous and give your email address as the password.

Let's see how to log in with ftp:

```
> ftp 10.1.1.1
> ftp pr1
```

Once connected to an FTP site, you can cd and ls your way around. Using the command get <filename> enables you to retrieve a file, and put <filename> enables you to send one from your directory to the remote system.

> Can I Secure FTP? So, how can I secure FTP if it is not secure? The answer is simple. You can use Secure FTP, or SFTP for short. If you have ssh installed you most likely have SFTP installed as it part of the same client package. If you do not have you can request it from your system administrator. Another program that you could use is also secure copy, or scp for short.