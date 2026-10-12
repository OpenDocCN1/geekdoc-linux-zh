You should automate this process and have Tripwire to run nightly or periodically and send you the reports via email. The sample entry in root's crontab file will accomplish the task:

```
0 0 * * * /usr/TSS/bin/tripwire --check
```

Tripwire examines file permissions, the unique size of each file, its hash and other properties that a malicious user could alter. You should install Tripwire or a similar system integrity checker on every new system that you set up.

# Cracking Bad Passwords

In addition to Tripwire, which takes a proactive stance against changes made by users, several programs are available that take a reactive approach to changes already made on the system. For instance, you can use the program crack to test the passwords of your users and see whether any of them “crack” when run against dictionary lists and when tested with a decryption algorithm. Many such programs are available that can use against your password files to check for weak or easily decipherable passwords.

You can get more information about the crack program from the developer’s site at http://www.users.discov.com/~crypto/index.html. The site provides links to FTP sites that provide the source code. I grabbed my copy from the site ftp://ftp.cerias.purdue.edu/pub/tools/unix/pwdutl s/crack/.

Install the program as you would any other. Place it in a secure location, such as root’s home directory, and then uncompress the file and its contents by using the standard command:

```
# gunzip -c crack5.0.tar.gz | tar xvf -
```

This will create a c50a/ directory. Change to this directory and read the manual.txt file for any specific notes. To generate the binary file, run the following command:

```
# ./Crack -makeOnly
```

This command may seem a bit backwards in that it appears you are building a pre-compiled binary and the executable is already present. However, the Crack command will simply create a new binary.