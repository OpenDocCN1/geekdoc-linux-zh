
## Continuing a Download

In the old days, if you were downloading a particularly large file (such as an ISO image of a CD or DVD), if the download stopped for some reason (a disconnected network or errant reboot), you needed to start all over. With `wget`, you can choose to restart a download and have it continue right where it left off. This has been a lifesaver for me on many occasions.

Let's say that you were downloading a 4GB DVD ISO image named `mydvd.iso` from the site `http://ftp.example.com` and you killed the `wget` process by mistake after about 3 GB of download. Make sure that your current directory is the one that contains the partially downloaded ISO. Then run the same `wget` command you did originally, adding the `-c` (continue) option as follows:

```bash
$ wget -c http://ftp.example.com/mydvd.iso
```

If you had not used the `-c` option, in this case, a new download would have started using the filename `mydvd.iso.1` to download to.

> **NOTE** Another command that you might be interested in, similar to `wget`, is the `curl` command. Like `wget`, `curl` can download files using the FTP or HTTP protocols. `curl` can also do multiple file transfers on the same connection.

## Using ssh for Remote Login/Remote Execution

Although the `telnet` and `rlogin` login commands and `rsh` remote execution command have been around much longer, the `ssh` command is the preferred tool for remote logins and executions. The reason is that `ssh` provides encrypted communication so you can use it securely over insecure, public networks between hosts that don't know each other.

In the following example, `ssh` is being used to log in to a computer named `sparky`. Because no user is specified, `ssh` tries to log in as the current user (which is the `root` user, in this case).

```bash
# ssh sparky
root@sparky's password:
```

If you wanted to log in as a different user, you could use the `-l` option. For example, to log in to the computer named `sparky` as the user named `jake`, you could type the following:

```bash
# ssh jake@sparky
jake@sparky's password:
```

The `ssh` command can also be used to execute a command on the remote computer. For example, if you wanted to monitor the messages file on a remote computer for a minute, you could type the following command:

```bash
# ssh root@sparky "tail -f /var/log/messages"
root@sparky's password:
```

After you typed the password in the preceding case, the last several lines of the /var/log/messages file on the remote computer would be displayed. As messages were received, they would continue to be displayed until you decided to exit (press `Ctrl`+`C` to exit the `tail` command).

> **NOTE** To learn how to use public keys for password-less login to `ssh`, refer to Chapter 13. Find out more about the `ssh` command from the SSH web site ([www.openssh.org](http://www.openssh.org)).

## Using `scp` for Remote File Copy

The `scp` command is a simple yet secure way of copying files among Linux systems. It uses the underlying `ssh` facility, so if `ssh` is enabled, so is `scp`. Here is an example of using `scp` to copy a file from one computer to another:

```bash
# scp myfile toys.linuxtoys.net:/home/chris
root@toys.linuxtoys.net’s password: ******
```

In this example, the file `myfile` is copied to the computer named `toys.linuxtoys.net` in the `/home/chris` directory. If you don't provide a username, `scp` assumes that you are using the current username. Unlike some tools that provide remote login, `scp` and `ssh` do allow you to log in as the `root` user over the network, by default. (Many people turn off this feature for security reasons.)

To use `scp` with a different username, you can append the username with an `@` character. For example, `chris@toys.linuxtoys.net:/home/chris` would attempt to log in as the user named `chris` to do the file copy.

The first time you connect to a remote computer using `scp` or `ssh`, those commands try to establish the authenticity of the remote host. If it cannot establish the host's authenticity, `scp` will display the RSA key fingerprint and ask you if you want to continue. If you type `yes`, `scp` will not question the authenticity of that computer again for subsequent `scp` commands.

However, if the RSA key fingerprint should change in the future for the remote computer (which will happen if, e.g., the operating system is reinstalled on that computer), `scp` will refuse to let you connect to that remote computer. To override that refusal, you need to edit your `$HOME/.ssh/known_hosts` file and delete the entry for the remote computer. You can then verify the authenticity of the remote computer and continue to use `scp`.

The `sftp` command, which also communicates using secure ssh protocols, is a command for copying files from an FTP server. It is considered a more secure way of getting files from an FTP server that has an `sshd` server running. The `sftp` command can be disabled by the server by commenting out the `sftp` line in the `sshd_config` directory.

## Using the “r” Commands: rlogin, rcp, and rsh

The rlogin, rcp, and rsh commands all use the same underlying security mechanism to enable remote login, remote file copy, and remote execution, respectively, among computers. These commands are included with CentOS to be compatible with legacy UNIX systems. Because “r” commands are inherently insecure, however, most people use ssh and scp commands to provide the same functionality in a more secure way.

## Summary

Most use of the World Wide Web centers on the Web browser. Firefox is fast becoming the most popular Web browser to use with CentOS and most other Linux systems and is accessible from a button on your desktop. Epiphany, Konqueror, and various text-based Web browsers are also available with CentOS.

Evolution, which can also be used for managing your e-mail, is now the preferred mail reader for CentOS. Thunderbird is the latest e-mail application from the Mozilla Project. There are also many text-based mail readers, such as Mutt, Alpine, and mail.

Command-line tools for downloading files include wget, ftp, and many others. A popular download tool, which offers both command-line and graphical interfaces, is BitTorrent. With BitTorrent, you not only download files, but also you can simultaneously upload the files you get to others.

Legacy remote login and file copy commands (rlogin, rcp, and rsh) are still available in CentOS. However, improved programs for remote login and file copy, such as ssh, scp, and sftp, are more often used today.

# Part II Using CentOS

After you typed the password in the preceding case, the last several lines of the /var/log/messages file on the remote computer would be displayed. As messages were received, they would continue to be displayed until you decided to exit (press `Ctrl`+`C` to exit the `tail` command).

Wait, I need to check the order. The OCR input has "Part II Using CentOS" on Page 373, but it seems like a header for a new section or a repeated header. Looking at the flow:
Page 372 ends with `ssh` execution.
Page 373 starts with "Part II Using CentOS" then continues the `ssh` paragraph. Then "Using scp...".
Page 374 ends with "Summary".
Page 375 is empty.
Page 376 is "Part III Administration".
Page 378 is "Chapter 9".

The header "Part II Using CentOS" on Page 373 appears to be a running header or a structural marker that got mixed into the text stream. Given the content immediately following it continues the `ssh` discussion from Page 372, and the subsequent sections are about `scp` and `r` commands which likely belong to the previous chapter (Chapter 8?), placing "Part II" in the middle of the text is structurally odd. However, the instruction says "Preserve original language and all information". If it's a running header, it might be noise, but if it's a section title, it should be kept. But looking at Page 376, "Part III Administration" is a major separator. "Part II Using CentOS" might be the start of the book's second part, but it's appearing in the middle of a technical chapter. It is highly likely this is a running header from the book layout that OCR picked up. I will treat major structural headers like "Part II" and "Part III" as top-level headers if they appear at the start of a logical section, but here "Part II" is interrupting a paragraph. 
Actually, re-reading carefully: 
Page 372: ... `ssh` command ...
Page 373: # Part II Using CentOS ... (Then continues the paragraph from 372). 
This suggests "Part II Using CentOS" is likely a running header that shouldn't break the paragraph flow, or it's a misidentified header. However, since I must preserve information and structure, and it is marked as a header (`#` in OCR), I will consider its placement. If I merge the paragraph across the page break, the header sits in the middle of the thought. 
Let's look at Page 376: `# Part III` `# Administration`. This clearly starts a new major section. 
The text on Page 373 "Part II Using CentOS" is likely the running head for the *entire* Part II of the book, which this chapter belongs to. In digital books, running heads are often extracted. I will remove the running head "Part II Using CentOS" from the flow of the text because it interrupts the paragraph "After you typed the password...", unless it is the start of a new chapter. But the chapter content (`scp`, `r` commands, `Summary`) seems to be the end of a chapter *within* Part II. 
Actually, looking at the "Summary" on Page 374, this concludes the chapter. The next page is empty. Then Page 376 starts Part III. 
So, the text from Page 372 to 374 is one continuous chapter. The "Part II Using CentOS" header on Page 373 is almost certainly a running header. I will exclude running headers that interrupt text flow to maintain semantic coherence, as per "correct OCR errors" and "identify headers". A header in the middle of a paragraph is an error/nuisance. 
However, "Part III" on Page 376 is a major divider. I will keep that. 
I will remove "Part II Using CentOS" because it breaks the paragraph continuity between Page 372 and 373.

Revised Plan:
1. Merge Page 372 and 373.
2. Remove the "Part II Using CentOS" line from the middle of the text.
3. Keep "Part III Administration" as a new section.
4. Keep "Chapter 9" as a new section.

Let's re-evaluate "Part II". If the book is structured as Part I, Part II, Part III... and this chapter is in Part II, the running head makes sense. I will omit it to preserve the paragraph flow.

[content]
## Continuing a Download

In the old days, if you were downloading a particularly large file (such as an ISO image of a CD or DVD), if the download stopped for some reason (a disconnected network or errant reboot), you needed to start all over. With `wget`, you can choose to restart a download and have it continue right where it left off. This has been a lifesaver for me on many occasions.

Let's say that you were downloading a 4GB DVD ISO image named `mydvd.iso` from the site `http://ftp.example.com` and you killed the `wget` process by mistake after about 3 GB of download. Make sure that your current directory is the one that contains the partially downloaded ISO. Then run the same `wget` command you did originally, adding the `-c` (continue) option as follows:

```bash
$ wget -c http://ftp.example.com/mydvd.iso
```

If you had not used the `-c` option, in this case, a new download would have started using the filename `mydvd.iso.1` to download to.

> **NOTE** Another command that you might be interested in, similar to `wget`, is the `curl` command. Like `wget`, `curl` can download files using the FTP or HTTP protocols. `curl` can also do multiple file transfers on the same connection.

## Using ssh for Remote Login/Remote Execution

Although the `telnet` and `rlogin` login commands and `rsh` remote execution command have been around much longer, the `ssh` command is the preferred tool for remote logins and executions. The reason is that `ssh` provides encrypted communication so you can use it securely over insecure, public networks between hosts that don't know each other.

In the following example, `ssh` is being used to log in to a computer named `sparky`. Because no user is specified, `ssh` tries to log in as the current user (which is the `root` user, in this case).

```bash
# ssh sparky
root@sparky's password:
```

If you wanted to log in as a different user, you could use the `-l` option. For example, to log in to the computer named `sparky` as the user named `jake`, you could type the following:

```bash
# ssh jake@sparky
jake@sparky's password:
```

The `ssh` command can also be used to execute a command on the remote computer. For example, if you wanted to monitor the messages file on a remote computer for a minute, you could type the following command:

```bash
# ssh root@sparky "tail -f /var/log/messages"
root@sparky's password:
```

After you typed the password in the preceding case, the last several lines of the /var/log/messages file on the remote computer would be displayed. As messages were received, they would continue to be displayed until you decided to exit (press `Ctrl`+`C` to exit the `tail` command).

> **NOTE** To learn how to use public keys for password-less login to `ssh`, refer to Chapter 13. Find out more about the `ssh` command from the SSH web site ([www.openssh.org](http://www.openssh.org)).

## Using `scp` for Remote File Copy

The `scp` command is a simple yet secure way of copying files among Linux systems. It uses the underlying `ssh` facility, so if `ssh` is enabled, so is `scp`. Here is an example of using `scp` to copy a file from one computer to another:

```bash
# scp myfile toys.linuxtoys.net:/home/chris
root@toys.linuxtoys.net’s password: ******
```

In this example, the file `myfile` is copied to the computer named `toys.linuxtoys.net` in the `/home/chris` directory. If you don't provide a username, `scp` assumes that you are using the current username. Unlike some tools that provide remote login, `scp` and `ssh` do allow you to log in as the `root` user over the network, by default. (Many people turn off this feature for security reasons.)

To use `scp` with a different username, you can append the username with an `@` character. For example, `chris@toys.linuxtoys.net:/home/chris` would attempt to log in as the user named `chris` to do the file copy.

The first time you connect to a remote computer using `scp` or `ssh`, those commands try to establish the authenticity of the remote host. If it cannot establish the host's authenticity, `scp` will display the RSA key fingerprint and ask you if you want to continue. If you type `yes`, `scp` will not question the authenticity of that computer again for subsequent `scp` commands.

However, if the RSA key fingerprint should change in the future for the remote computer (which will happen if, e.g., the operating system is reinstalled on that computer), `scp` will refuse to let you connect to that remote computer. To override that refusal, you need to edit your `$HOME/.ssh/known_hosts` file and delete the entry for the remote computer. You can then verify the authenticity of the remote computer and continue to use `scp`.

The `sftp` command, which also communicates using secure ssh protocols, is a command for copying files from an FTP server. It is considered a more secure way of getting files from an FTP server that has an `sshd` server running. The `sftp` command can be disabled by the server by commenting out the `sftp` line in the `sshd_config` directory.

## Using the “r” Commands: rlogin, rcp, and rsh

The rlogin, rcp, and rsh commands all use the same underlying security mechanism to enable remote login, remote file copy, and remote execution, respectively, among computers. These commands are included with CentOS to be compatible with legacy UNIX systems. Because “r” commands are inherently insecure, however, most people use ssh and scp commands to provide the same functionality in a more secure way.

## Summary

Most use of the World Wide Web centers on the Web browser. Firefox is fast becoming the most popular Web browser to use with CentOS and most other Linux systems and is accessible from a button on your desktop. Epiphany, Konqueror, and various text-based Web browsers are also available with CentOS.

Evolution, which can also be used for managing your e-mail, is now the preferred mail reader for CentOS. Thunderbird is the latest e-mail application from the Mozilla Project. There are also many text-based mail readers, such as Mutt, Alpine, and mail.

Command-line tools for downloading files include wget, ftp, and many others. A popular download tool, which offers both command-line and graphical interfaces, is BitTorrent. With BitTorrent, you not only download files, but also you can simultaneously upload the files you get to others.

Legacy remote login and file copy commands (rlogin, rcp, and rsh) are still available in CentOS. However, improved programs for remote login and file copy, such as ssh, scp, and sftp, are more often used today.

# Part III
# Administration

**IN THIS PART**

- Chapter 9 **Understanding System Administration**
- Chapter 10 **Setting up and Maintaining User Accounts**
- Chapter 11 **Automating System Tasks**
- Chapter 12 **Creating Backups and Restoring Data**
- Chapter 13 **Security**

# Chapter 9

## Understanding System Administration

CentOS, like other Linux and UNIX systems, is intended for use by more than one person at a time. Multiuser features allow many people to have accounts in Linux, with their data kept secure from others. Multitasking allows many people to use the computer at the same time. Sophisticated networking protocols and applications make it possible for a Linux system to extend its capabilities to network users and computers around the world. The person assigned to manage all of this stuff is referred to as the *system administrator*.

Even if you are the only person using a Linux system, system administration is still set up to be separate from other computer use. To do most administrative tasks, you need to be logged in as the *root* user (also referred to as the *super user*) or gain temporary root privilege. Other users cannot change, or in some cases, even see some of the configuration information for a Linux system. In particular, security features such as passwords are protected from general view.

This chapter describes the general principles of administering a CentOS system. In particular, this chapter covers some of the basic tools you need to administer your Linux system. It also helps you learn how to work with file systems and monitor the setup and performance of your Linux system.

Security Enhanced Linux (SELinux) adds another dimension to administering a CentOS system. Instead of giving the *root* user full control of the entire Linux system, access to data, programs, devices, and processes can be assigned to different roles. CentOS is delivered with only a limited set of SELinux features turned on, so the *root* user maintains most of its traditional role whether SELinux is off or on. SELinux is described at the end of this chapter.

## IN THIS CHAPTER

- Using the root login
- Administrative commands, configuration files, and log files
- Graphical administration tools
- Working with the file system
- Working with hardware devices
- Monitoring system performance
- Managing battery power on laptops
- Using Security Enhanced Linux
