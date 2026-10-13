
![](img/c2419364ebb911c809b6a79991707c27_490_0.png)

## Tip
If you use shadow passwords and want to run Crack, you need to use a support script called shadmrg (found in the Scripts directory) to merge the /etc/passwd and /etc/shadow files. The merged output typically is sent to STDOUT, so you have to point it to a file, which you can then use with Crack as the input password file.

Crack will start cracking your passwords. If you have a lot of user accounts in your password file, Crack might take a long time to complete the job. That's why Crack automatically runs in the background. You can also specify a few command-line options to Crack to control some of its behavior. Run Crack without any arguments to see a list of command-line options.

## Getting Crack's output
After you run Crack, it creates output in two files: out.PID and out.host-name/PID. For example, the output files could be out.5678 and out.picaso.nitec.com/5699, where picaso.nitec.com is the name of the host running Crack. Listing 15-8 shows an example of a Crack output file.

### Listing 15-8 Example Crack Output File
```
join: User apache (in /etc/passwd) has a locked password:- !!
join: User uucp (in /etc/passwd) has a locked password:- *
join: User operator (in /etc/passwd) has a locked password:- *
join: User ftp (in /etc/passwd) has a locked password:- *
join: User bin (in /etc/passwd) has a locked password:- *
join: User daemon (in /etc/passwd) has a locked password:- *
join: User adm (in /etc/passwd) has a locked password:- *
join: User lp (in /etc/passwd) has a locked password:- *
join: User sync (in /etc/passwd) has a locked password:- *
```

### Listing 15-8 Continued
```
join: User shutdown (in /etc/passwd) has a locked password:- *
join: User halt (in /etc/passwd) has a locked password:- *
join: User mail (in /etc/passwd) has a locked password:- *
join: User nobody (in /etc/passwd) has a locked password:- *
join: User news (in /etc/passwd) has a locked password:- *
join: Guessed pikeb (/bin/tics in /etc/passwd) {book} NssDrM.TU/EPc
```

The date stamp field that appears right after join: was removed to reduce line width. When Crack reports that a password is locked, it means that the password is set to *; in other words, the user account cannot be used to log in. The preceding last line is the most interesting one. It says that Crack has guessed the password (book) for user pikeb.

After you know which user passwords are crackable, lock out the account right away by using * as the password, and contact the user personally to discuss security. If that's not possible, notify the user to change the password immediately. If the user does not change the password in a given time frame, definitely lock out the account and advise your superiors on the matter.

Passwords are not the only weak points in a system. To find many other potential security holes, you need COPS.

## Having COPS around
COPS is a set of tools that attempts to locate potential security holes in a system. Among other things, these tools focus on detecting potential security problems that can surface from file/directory/device permissions, passwords, init files in the /etc/rc.d directory, cron configuration, and anonymous FTP setup. Basically, the purpose of COPS is to detect potential security problems and warn you about them. It does not fix any of the problems that it detects.

## Installing COPS
I have not yet seen an RPM-packaged version of COPS. So, you have to get a general COPS distribution from the following FTP site: ftp://ftp.cert.org/pub/tools/cops/.

Download the latest COPS distribution and uncompress and extract the files to an appropriate directory on your system.

The COPS distribution includes two versions of the same software. One version is written primarily in C, and the other is written primarily in Perl. You can run a version as long as you have either Perl or a C compiler, either of which is practically standard in Red Hat Linux. This discussion explains how to use the C version. If you are interested in running the Perl version of the software, read the bundled README files for the Perl version. You will also find the Perl version of the software in a perl subdirectory of your installation directory.

To configure the C version of COPS, do the following:

- 1. First, run the following script from the installation directory:
  
      `./reconfig`
  
      This adjusts a few paths for binaries, such as awk, in some scripts to match your system.
  
- 2. Next, modify the makefile in the docs directory to remove the -ms from the ROFFLAGS = -ms line. You don't need to do this if you have installed the -ms package for nroff. Then, run the following from the installation directory:
  
      `./make all`
  
- 3. Edit the cops shell script and modify the following lines:
  
      `SECURE=/usr/foobar`
      `SECURE_USERS="foo@bar.edu"`
  
- 4. Change the first line so that the directory is the fully qualified directory name of your installation path. For example, if you installed COPS in the /usr/local/security/cops directory, then set SECURE to that directory. Set the second line to your e-mail address where the COPS output will be sent. If you do not want to receive the report in e-mail format, modify MMAIL=NO or change the line to be MMAIL=YES to receive the report via e-mail.

- 5. If you decide not to receive e-mailed reports, you can find the report files in the $SECURE/(short hostname) directory. For example, if your system's host name is picaso.nitec.com, and SECURE is set to /usr/local/security/cops, the report file will be stored in the /usr/local/security/cops/picaso/ directory. The report filename is created using the year_month_day format (for instance, 1999_Feb_25).

- 6. If you plan to use the Crack program as your password-cracking software, you can comment out the line (by inserting a # character in front of the line) that starts $SECURE/pass.chk. If you run an anonymous, FTP site, you can modify the line that starts with $SECURE/ftp.chk to read $SECURE/ftp.chk -a.

## Running COPS
Running COPS is quite simple; run it from the installation directory as follows:

```
./cops
```

Listing 15-9 shows an example COPS report.

### Listing 15-9 An Example COPS Report
```
ATTENTION:
Security Report for Thu Jan 29 10:35:44 PST 1998
from host picaso.nitec.com

Warning! /dev/fd0 is _World_ readable!
Warning! /etc/security is _World_ readable!
Warning! /etc/crontab is _World_ readable!

ATTENTION:
COPS Security Report for Thu Jan 29 10:34:39 PST 1998
from host picaso.nitec.com

replaced -rw-r--r-- root  root Jan 28 23:22:01 1998
/etc/passwd
```
```
removed -r------ root  root Dec 20 13:31:36 1998
/etc/shadow
```

COPS just finds the problems, it doesn't fix them. It is up to you to investigate and fix them. Run COPS on a regular basis by setting it up as a cron job so that you get regular reports on potential problems before they are exploited by the bad guys.

## Back Up and Backtrack Everything
The most important security advice anyone can give you is to regularly back up all of your files. Here is what I recommend:

- Create a maintainable backup schedule for your system.
- Perform incremental backups on weekdays and schedule a full backup over the weekend. I prefer removable-media-based backup equipment, such as 8mm tape drives or DAT drives.
- Having a removable backup medium enables you to take the backup away from the location and store it in a secure offsite location.
- Periodically check that your backup mechanism is functioning as expected. Make sure you're able to restore files from randomly selected backup media.
- You may recycle backup media, but make sure you know the usage limits that the media manufacturer claims.
- Protecting your system involves more than simply keeping bad guys out. You want to protect your data from other sorts of disasters, as well, and good, periodic backups give you that protection.

Another type of “backup” you should get used to doing is backtracking your work as a system administrator. Document everything you do, especially work that you do as a superuser. This enables you to trace problems quicker. One of the things that I like to do when performing system administration is to keep a large history setting (a shell feature that remembers N number of your last commands) and periodically print the history in a file or on paper. You can also use the script command to record everything you do while using privileged accounts.
