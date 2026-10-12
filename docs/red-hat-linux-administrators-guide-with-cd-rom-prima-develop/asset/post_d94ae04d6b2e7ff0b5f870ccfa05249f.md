
After locating the file in question, downloading involves a series of specific commands. The get and put commands are the simplest to use with FTP. If you wish to download a particular file, enter get <file name>. If you have access to that directory and wish to upload a file from your own machine, enter put <file name>. Make sure that the file you are uploading is located in the same directory that you were in when you connected to the FTP server.

If you need to change your local directories, simply enter lcd /home/<user name> or lcd <directory name>/. Changing directories on the remote FTP server is the same as under regular directories. A simple cd command followed by the directory name will work from that server also. The ls command is also useful to view the contents of the remote directory.

When you are downloading or uploading files, do not forget the bin and ascii commands if transferring data between UNIX and non-UNIX machines. The bin command stands for binary whereas the ascii command stands for simple ASCII text files. Depending on the type of file you are sending, convert the method of transport to the file type. If moving data between two Linux boxes you never need worry about setting the bin or ascii commands.

Some additional examples that help in downloading and uploading files are the following commands. To view the progress your download is making rather than waiting for the transfer to complete, use the hash or tick commands. Much like the hash option when using the rpm command, the hash command shows a steady stream of hash marks across your screen representing bytes of data received. The tick command uses a numeric format to show how many bytes of data have been downloaded. In this manner, the command's output presents a better representation of how far along your download is and how much is left.

When downloading multiple files from a location instead of just one, you should use the mget or mput command. Here you can use wildcard options such as the following:

```
mget linux-2.2.*
```

If you are attempting to download all copies of the stable Linux kernel from the FTP site, the program will ask, after each download is complete, whether you want to download the next file. Depending on your answer, the program will either download the files successively or skip to the next file.

If you do not want the program to prompt you every time, you can use the prompt command to turn this feature off. Then the program will download all the files in rapid succession. To turn any of these features back on, simply retype the command. FTP will inform you that that particular feature has been turned on.

## Using GUI FTP Clients

For many converts to Linux, command-line programs are not enough, even though they may be more flexible to use. These new users require simplified GUIs. For this purpose, many FTP clients now run under the X Window interface. One of the better clients is IgllooFTP. This client provides all the features of the command-line interface and yet is simple enough that anyone can use it. It is actually better than related counterparts that run under Windows. Because it is designed for Linux, it is more stable and robust than WS_FTP, one of the most popular Windows FTP clients. If you use FTP often and are frequently in the X Window environment, you may want to try either this FTP client or one of the many others.

The types of programs available for Linux users to access other servers or to gain access to Internet sites are manifold. It requires but a little research and testing to discover quickly how broad the field is for Internet use under Linux. Because Linux was designed for use as a server, you can provide the same services to others as are available for your own use.

## Conclusion

This chapter focused on creating dial-up networks and granting additional connectivity between the home, office, and Internet. As your skills in accessing the Internet from a Linux-based machine grow, you will also want to reciprocate in the information that you download. The next chapter focuses on one of the main bonding elements of the Internet community, e-mail. In particular, the chapter examines the sendmail program, a mainstay in electronic mail transfer agents (MTAs). Chapter 17 looks at how sendmail is installed by Red Hat, how to customize it to suit, how to free it up for your own use, and how to lock it down for added security.

![](img/a0884097af3186d9b4f616aaa3f065b0_646_0.png)

# Chapter 17 E-mail

Electronic mail has become an integral part of most people’s lives. It links people from all over the globe, assists in gathering information we need, and provides a new means of communication that makes anonymous the sender from the sendee. It is known for both good and bad. From out of this free exchange of transmissions there has also arisen a barrage of junk and unsolicited electronic messages. Understanding how sendmail, the de facto mail utility for Linux, functions and how you as an administrator can tailor it to your needs is a crucial part of this chapter.

This chapter will examine the following areas:

- Obtaining the sendmail program and installing it via source or RPM
- Configuring the various enabling options for your domain
- Running sendmail from the command line or as a daemon
- Eliminating spam or unsolicited e-mail from your system
- Testing new configurations in your sendmail setup
- Sending mail from virtual domains within your system
- Checking and forwarding e-mail from your machine and others

## Understanding Mail Transfer Agents

As one of the oldest and most tried and proven mail transfer agents currently available, sendmail has an option for nearly every situation. Due to its age and the many incarnations it has undergone, it not only has become a standard bearer for e-mail delivery, but has so many features and variables that it requires a full chapter to cover the greater part of the many features it offers.

It is argued that sendmail is too convoluted for the present-day Internet. Many would prefer substituting a simpler program to handle the flood of e-mail currently awash through the networks. But with the many varying servers and e-mail clients delivering mail throughout the world, none can match sendmail in its robustness and stability.

One of the most popular uses of Linux is that of a mail server. Because of its dependability under high stress and load conditions and due to its low cost, it is customarily chosen to run the mail server of a company or organization. The preferred Mail Transfer Agent (MTA) that is responsible for handling incoming mail and properly sending it back out again is sendmail. Think of a mail server as one small post office where letters come in from all over the world. The sendmail program tackles all the traffic and properly sorts the messages either to drop them off within a local post office box or to ship them out again to a client that has relocated to another server. Such is the task and capacity of sendmail.

## Exploring the sendmail Program

The sendmail program is free for all to use. Though it has branched off subsidiary versions for commercial use and development, the main source code is still available to the public for download. Since it is licensed in its open-source incarnation, it too requires that any changes or improvements made to it must be released back to the community for its acceptance and/or disapproval. The developers, though, have final say in how sendmail will function and can revoke any change if they feel it compromises the security of the program. These checks and balances help to make sendmail not only more dependable but more efficient.

It is beyond the scope of this chapter to take an in-depth look at how each individual section of sendmail functions. Rather than look at the nuances of the program, this chapter instead examines some of the methods used to create a functioning version of sendmail, customizing its features under Linux while examining other mail programs. The chapter also looks at security issues posed by mail programs and at the way that mailing lists operate. Also, the chapter examines some of the methods employed both to view and handle mail on the server and client side. These methods include the use of POP3 and IMAP programs that manipulate incoming mail, along with the use of the pine program, which allows users to read and answer mail directly on the server.

### Installing sendmail

The sendmail program is a rather complicated mailing utility, but it is by far the most versatile and robust program available. What follows in this section are instructions for setting up sendmail on a standard Red Hat Linux machine. With most every distribution of Red Hat, sendmail comes preinstalled.
