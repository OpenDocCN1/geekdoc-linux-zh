
is because `faxmail` is being invoked with the `-n` flag to suppress coversheet generation. The argument `$1` is replaced by `$u`, which is the destination fax number. The argument `$2` is replaced by `$h`, which is the UID of the sender.

## Adding HylaFAX Support to Sendmail Using M4

The steps involved in adding HylaFAX support to sendmail on a Red Hat Linux system are quite easy. They are the following:

1. Change your current directory to the directory containing m4 definition files with the command `cd /usr/lib/sendmail.cf/cf/`.

2. Make a copy of your current Red Hat m4 configuration file with the command `cp redhat.mc redhat+hylafax.mc`.

3. Edit the new m4 definition file and add the following line:

   ```m4
   MAILER(fax)
   ```

4. Run the make command:

   ```sh
   # make redhat+hylafax.cf
   rm -f redhat+hylafax.cf
   m4 ../m4/cf.m4 redhat+hylafax.mc > redhat+hylafax.cf || \
       (rm -f redhat+hylafax.cf && exit 1)
   chmod 444 redhat+hylafax.cf
   ```

5. Browse the newly created configuration file `redhat+hylafax.cf`, and make sure you see a mailer definition, Mfax, address rewriting rules to support the `.FAX` address format, and the pseudo domain definition CPFAX. In the Mfax mailer section, verify the path to the faxmail program is correct. If it is not correct, fix it by hand. Now you can install the newly created sendmail configuration file. First, stop sendmail:

   ```sh
   # /etc/rc.d/init.d/sendmail stop
   ```

6. Save the current configuration file:

   ```sh
   # mv /etc/sendmail.cf /etc/sendmail.cf.old
   ```

7. Copy the new configuration file to sendmail.cf:

   ```sh
   # cp redhat+hylafax.cf /etc/sendmail.cf
   ```

8. Restart the sendmail daemon:

   ```sh
   # /etc/rc.d/init.d/sendmail start
   ```

## Testing the E-mail-Fax Gateway

You are now ready to test the newly configured E-mail-Fax gateway. This can be done using any mail program. The command line mail utility `/bin/mail` is very handy for quickly sending email from the command line. Run the following command:

```sh
# mail -v joe@551212.fax < test
```

Needless to say, you must replace the destination fax number in the above-mentioned command with a valid fax number where you can receive faxes.

Check the send queue on the fax server by running the `faxstat` command as follows:

```sh
faxstat -h faxhost.bwc.org -s
```

Again replace the name of the fax host with the correct name of your fax server.

If you see the job either queued or being processed, you have successfully installed an email-fax gateway.

**Tip**

For `faxmail` to work, you must ensure users can access the fax server without supplying passwords. This is necessary because the `faxmail` program runs with the UID of the user submitting the job through `sendmail`. The hosts file on the fax server must allow access from all users without asking for a password. Because the `faxmail` program runs in the background and is not interactive, it is not possible to collect a password from the user and supply it to the `hfaxd` process on the fax server.

## HylaFAX Transfer Logs

HylaFAX maintains accurate logging of all faxes sent and received in the log file `/var/spool/fax/etc/xferfaxlog`. The default name of the file is `xferlog`, which has been changed in RPM packages to `xferfaxlog`, to distinguish it from the `xferlog` file used by WU-FTPD.

This file contains one line per inbound or outbound call, except for faxes received by polling, when multiple entries may be present for a single call. The records are fixed format, with fields separated by the tab character.

A transmission record has the following format:

```text
date  SEND  commid  modem  jobid  jobtag  sender  dest-number  CSI  params  #pages  job-time contime reason
```

A receive record has the following format:

```text
date  RECV  commid  modem  <null>  <null>  fax  local-number  TSI  params  #pages  jobtime contime reason
```

Two typical sample entries in the `xferfaxlog` file are shown below.

```text
# more xferfaxlog
03/20/00 14:59  SEND   00000002   ttyS1   1   ""   gautam  "8358525" "972 4 8358525"   33031   1   0:55   0:37   ""
03/20/00 15:46  RECV   00000003   ttyS1   ""   fax   "+972.4.8331039" "+972 4 8358591"   258   1   1:02   1:02   ""
```

As is clearly evident the data contains valuable information such as the call time, user name, local and remote phone numbers, number of pages sent or received, and the connect time. If necessary, this data can be easily processed by a script to generate billing information.

## HylaFAX cron Jobs

HylaFAX comes with two programs that run from crond. One runs once a day, and the other runs every hour. Let us take a brief look at what these programs do.

The `/usr/sbin/faxqclean` program runs every hour from crond. It processes completed jobs and removes document files that are not referenced. faxqclean scans the `/var/spool/fax/doneq` directory and processes each file according to the doneop specified in the job description file. Jobs marked for removal are deleted and any references to them are removed.

Jobs marked for archival are moved into the `/var/spool/fax/archive` directory. After scanning the doneq directory, faxqclean examines the `/var/spool/fax/docq` directory. Files that are not referenced by any job and files that are older than a specified threshold are deleted.

The `/usr/sbin/faxcron` script runs once a day from crond. It generates daily and weekly statistics about faxes sent and received. It reports any recent calls that failed suspiciously and returns the associated trace log files. It purges data older than 30 days from the remote machine information directory. It deletes information older than 30 days from session trace log files. It cleans the `/var/spool/fax/tmp` directory, removing files that are older than a day. It cleans the `/var/spool/fax/recv` directory by removing received faxes that are older than 7 days. It reports sites that are currently rejecting faxes. It makes sure all session log files are owned by the user fax and have file protection mode 644. A summary report is mailed to the Fax Master.

## Troubleshooting HylaFAX

We will now discuss some common problems you may face when setting up or running HylaFAX. We will look at the server-side and client-side problems separately. For effective troubleshooting, you must have a good overall understanding of the various components of HylaFAX.

The client-side components are sendfax, faxstat, faxrm, and sendpage.

The server-side components support four distinct job functions. The hfaxd daemon’s function is to communicate with the client programs. The faxq daemon schedules outbound jobs. The faxsend and pagesend programs handle delivery of faxes and pages. The faxgetty daemon services the modems and receives inbound faxes.

In addition, periodic processes such as faxqclean and faxcron are run from crond.

When you are having a problem, it is first necessary to identify whether it is a client-side problem, a server-side problem, or a problem relating to periodic jobs that run from crond.

Generally, HylaFAX is a very stable and robust piece of software and is designed for uninterrupted operation. Once set up correctly, it requires little or no intervention from the system administrator.

### An Example of a Client-Side Problem

A client cannot contact the fax server. You run the `faxstat` program and see output similar to the following:

```text
$ faxstat
Can not reach server at host 'faxhost1.bwc.org', port 4559.
```

Make sure the server name is correct. If not, set the proper name of the server in `/usr/share/hyla.conf`, or `.hylarc`, or the environment variable FAXSERVER. General network connectivity problems cannot be ruled out. Use ping and other TCP/IP diagnostics programs to verify the remote fax server can be reached from the client.

After fixing the server name, or any network problems, run `faxstat` again and you should see something like the following:

```text
$ faxstat
HylaFAX scheduler on orion.bwc.org: Running
Modem ttyS1 (+972 4 833-1029): Running and idle
```

If the output is as shown below, then your client is communicating with the server but there is a problem on the server:

```text
HylaFAX scheduler on faxhost.bwc.org: Not running.
```

### An Example of a Server-Side Problem

If `faxstat` output shows the scheduler is not running such as shown in the faxstat output below, then the `faxq` daemon is either dead or has a problem:

```text
$ faxstat
HylaFAX scheduler on orion.bwc.org: Not running
Modem ttyS1 (+972.4.8331039): Running and idle
```

To fix this problem, do a process listing and check whether the `faxq` process is running. If it is not running, you can start it by running the following command as the root user:

```sh
# /usr/sbin/faxq
```

The program will put itself in the background and change its UID to fax.

If the ps output shows faxq is running, but faxstat reports the scheduler is not running, you should check the server tracing log for faxq to see what the problem is. `faxstat` communicates with hfaxd on the fax server to get the status information. hfaxd decides if faxq is running based on whether it can open the FIFO special file `/var/spool/fax/FIFO`. Make sure this file is the correct type and has the appropriate permissions. The proper ownership and permissions of the FIFO file are as shown by the following ls listing:

```text
# ls -l /var/spool/fax/FIFO
prw------- 1 uucp uucp 0 Mar 22 17:43 FIFO
```

faxq creates the FIFO file when it starts up if it does not already exist. If there is a problem, stop faxq, stop hfaxd, remove the file, and restart faxq and hfaxd using the following commands:
