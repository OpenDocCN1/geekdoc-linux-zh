
# /usr/sbin/faxquit
# /etc/rc.d/init.d/hylafax stop
# rm -f /var/spool/fax/FIFO
# /etc/rc.d/init.d/hylafax start

After running faxquit verify the faxq process has really terminated. Otherwise you may need to use kill -9 to end this process. This is an extreme example and probably will never happen. Before killing faxq in this way make sure no outbound jobs are in progress. Killing faxq while outbound jobs are processing can leave the system in an inconsistent state, and can require a reboot of the server.

## DEBUGGING COMMUNICATION PROBLEMS

Modem communication problems can be debugged by looking at session log files. Session log files are stored in the /var/spool/fax/log directory. Session logs are easy to understand. A sample extract of a session log file follows:

```text
Mar 20 14:59:22.38: [ 492]: SESSION BEGIN 00000002 97248358525
Mar 20 14:59:22.38: [ 492]: SEND FAX JOB 1 DEST 8358525 COMMID 00000002
Mar 20 14:59:22.38: [ 492]: DELAY 260 ms
Mar 20 14:59:24.98: [ 492]: <-- [15:ATE0V1Q0S0=0H0\r]
Mar 20 14:59:24.99: [ 492]: <-- [2:OK]
Mar 20 14:59:24.99: [ 492]: --> [21:AT+FCLASS=2&CID=1\r]
Mar 20 14:59:25.00: [ 492]: <-- [2:OK]
Mar 20 14:59:25.00: [ 492]: --> [12:AT+FCLASS=1\r]
Mar 20 14:59:25.01: [ 492]: <-- [2:OK]
Mar 20 14:59:25.01: [ 492]: <-- [5:ATM0\r]
Mar 20 14:59:25.02: [ 492]: <-- [2:OK]
Mar 20 14:59:25.02: [ 492]: --> [12:AT+FCLASS=1\r]
Mar 20 14:59:25.15: [ 492]: DIAL 8358525
Mar 20 14:59:25.15: [ 492]: --> [12:ATD8358525\r]
Mar 20 14:59:40.22: [ 492]: --> [7:CONNECT]
Mar 20 14:59:41.56: [ 492]: <-- [2:OK]
Mar 20 14:59:41.56: [ 492]: --> [9:AT+FTH=3\r]
Mar 20 14:59:41.57: [ 492]: --> [7:CONNECT]
Mar 20 14:59:42.26: [ 492]: <-- [2:OK]
Mar 20 14:59:42.26: [ 492]: REMOTE CSI "972 4 8358525"
Mar 20 14:59:42.27: [ 492]: <-- [9:AT+FNH=3\r]
Mar 20 14:59:42.52: [ 492]: --> [7:CONNECT]
Mar 20 14:59:42.52: [ 492]: <-- [2:OK]
Mar 20 14:59:42.52: [ 492]: REMOTE best rate 9600 bit/s
Mar 20 14:59:42.52: [ 492]: REMOTE max page width 1728 pixels in 215 mm
Mar 20 14:59:42.52: [ 492]: REMOTE max unlimited page length
Mar 20 14:59:42.52: [ 492]: REMOTE best vres 7.7 line/mm
Mar 20 14:59:42.52: [ 492]: REMOTE best format 1-D MR
Mar 20 14:59:42.52: [ 492]: REMOTE best 20 ms, 10 ms/scanline
Mar 20 14:59:42.52: [ 492]: USE 9600 bit/s
Mar 20 14:59:42.52: [ 492]: USE 20 ms, 10 ms/scanline
Mar 20 14:59:42.52: [ 492]: SEND file "docq/doc1.ps;31"
Mar 20 14:59:42.52: [ 492]: USE page width 1728 pixels in 215 mm
Mar 20 14:59:42.52: [ 492]: USE unlimited page length
Mar 20 14:59:42.52: [ 492]: USE 7.7 line/mm
Mar 20 14:59:42.52: [ 492]: USE 1-D MR
Mar 20 14:59:42.52: [ 492]: SEND training at v.29 9600 bit/s
Mar 20 14:59:42.52: [ 492]: <-- [9:AT+FH=3\r]
Mar 20 14:59:42.59: [ 492]: --> [7:CONNECT]
Mar 20 14:59:42.56: [ 492]: <-- data [23]
Mar 20 14:59:42.56: [ 492]: <-- data [2]
Mar 20 14:59:44.38: [ 492]: --> [7:CONNECT]
Mar 20 14:59:44.38: [ 492]: <-- data [6]
Mar 20 14:59:44.38: [ 492]: <-- data [2]
Mar 20 14:59:44.79: [ 492]: --> [2:OK]
Mar 20 14:59:44.79: [ 492]: DELAY 75 ms
Mar 20 14:59:44.87: [ 492]: <-- [10:AT+FT=96\r]
Mar 20 14:59:44.91: [ 492]: --> [7:CONNECT]
Mar 20 14:59:44.91: [ 492]: <-- data [1024]
Mar 20 14:59:44.91: [ 492]: <-- data [776]
Mar 20 14:59:44.91: [ 492]: <-- data [2]
Mar 20 14:59:46.86: [ 492]: <-- [9:AT+FRH=3\r]
Mar 20 14:59:47.47: [ 492]: --> [7:CONNECT]
Mar 20 14:59:48.35: [ 492]: --> [2:OK]
Mar 20 14:59:48.35: [ 492]: TRAINING succeeded
Mar 20 14:59:48.35: [ 492]: <-- [10:AT+FT=96\r]
Mar 20 14:59:48.38: [ 492]: --> [7:CONNECT]
Mar 20 14:59:48.38: [ 492]: SEND begin page
Mar 20 14:59:48.39: [ 492]: <-- data [1027]
... ... ...
Mar 20 15:00:06.18: [ 492]: <-- data [270]
Mar 20 15:00:06.67: [ 492]: SENT 25870 bytes of data
Mar 20 15:00:06.67: [ 492]: <-- data [1033]
Mar 20 15:00:07.15: [ 492]: <-- data [1029]
Mar 20 15:00:08.12: [ 492]: <-- data [124]
Mar 20 15:00:08.12: [ 492]: SENT 2172 bytes of data
Mar 20 15:00:08.12: [ 492]: SEND 10 RTC
Mar 20 15:00:08.12: [ 492]: <-- data [29]
Mar 20 15:00:08.12: [ 492]: <-- data [2]
Mar 20 15:00:08.12: [ 492]: SEND end page
Mar 20 15:00:12.24: [ 492]: --> [2:OK]
Mar 20 15:00:12.24: [ 492]: DELAY 95 ms
Mar 20 15:00:12.34: [ 492]: SEND end of (no more pages or documents)
Mar 20 15:00:12.34: [ 492]: <-- [9:AT+FH=3\r]
Mar 20 15:00:12.38: [ 492]: --> [7:CONNECT]
Mar 20 15:00:12.38: [ 492]: <-- data [3]
Mar 20 15:00:12.38: [ 492]: <-- data [2]
Mar 20 15:00:13.70: [ 492]: --> [2:OK]
Mar 20 15:00:13.70: [ 492]: <-- [9:AT+FRH=3\r]
Mar 20 15:00:14.20: [ 492]: --> [7:CONNECT]
Mar 20 15:00:15.12: [ 492]: --> [2:OK]
Mar 20 15:00:15.12: [ 492]: SEND recv MCF (message confirmation)
Mar 20 15:00:15.12: [ 492]: SEND FAX (00000002): FROM root@orion.bwc.org TO 8358525 (page 1 of 1 sent in 0:33)
Mar 20 15:00:15.12: [ 492]: SEND FAX (00000002): FROM root@orion.bwc.org TO 8358525 (docq/doc1.ps;31 sent in 0:33)
Mar 20 15:00:15.12: [ 492]: <-- [9:AT+FH=3\r]
Mar 20 15:00:15.16: [ 492]: --> [7:CONNECT]
Mar 20 15:00:15.16: [ 492]: <-- data [3]
Mar 20 15:00:15.16: [ 492]: <-- data [2]
Mar 20 15:00:16.47: [ 492]: --> [2:OK]
Mar 20 15:00:16.47: [ 492]: <-- [5:ATH0\r]
Mar 20 15:00:17.15: [ 492]: --> [2:OK]
Mar 20 15:00:17.15: [ 492]: SESSION END
```

Messages sent to the modem are the lines marked with a <- (left-arrow). Data received from the modem are the lines marked with a -> (right-arrow). Timestamps show the date and time. Time stamps are displayed with 10 millisecond precision, which is typical for real time clocks on UNIX systems. Unimportant binary data is generically shown as data.

These log files can pinpoint modem-related problems when talking to different fax machines and fax modems. It is highly recommended that you do not use a generic modem on your fax server. Trying to save money on a modem is a sure way of introducing problems. Buy a good brand name, high-end modem and you will save yourself a lot of aggravation. A list of modems that have been used with HylaFAX can be found on the HylaFAX Web site at

```text
http://www.hylafax.org/modems.html
```

## USING EFAX

By using Efax you can easily set up the following:

- A fax server using the Linux print spool to send faxes in the same way you print documents.
- An email-to-fax gateway using the additional Qfax software.
- An automated logging system that can produce logs of user’s calls.

Although Efax does not offer the features needed for a large enterprise faxing system and you should be considering a full-scale product such as HylaFAX or Fax2Send for larger installations, Efax is easy to set up and use for small installations. Specifically, Efax is not ideally suited to sites which need to use a fax server with multiple fax modems and is not well-suited to the task of acting as an incoming fax server which can automatically route incoming faxes by email.

### INSTALLING EFAX

The current version of Efax is 0.9 and is available as the file efax-0.9.tar.gz from http://metlab.unc.edu/pub/Linux/apps/serialcomm/fax/efax-0.9.tar.gz. Download the file and extract it in a convenient location with the command:

```text
# tar xzvf efax-0.9.tar.gz
```

Efax will be extracted into the directory efax-0.9. Change to this directory and compile the software with the following command:

```text
# make
```

Install the compiled binaries, the Efax scripts and the manual pages with the command:

```text
# make install
```

The following Efax files will be installed in `/usr/bin`:

- **efax**: Sends and receives faxes
- **efix**: Converts between the fax format and text, bitmap and grayscale formats
- **fax**: Main control script for making, sending, viewing, receiving, and printing faxes

### Configuring Efax

To use Efax for sending and receiving faxes from the local system where it is installed with a fax modem requires minimal configuration. You only need to edit the `/usr/bin/fax` script with your preferred text editor and set the value of the following variables as outlined in the script:

- **DEV**: Your modem device. Typically this will be a serial device such as `ttys0` or `ttys1`.

  > **Note**
  > 
  > The comments about the DEV variable refer to dial-out devices such as `cua0` and `cua1`. These are references to older versions of Linux that distinguished between outgoing and incoming serial devices. In all current versions of Linux, this distinction no longer exists.

- **FROM**: Your fax number that should be written in standard international form. This format allows for numbers, spaces, and the plus sign (+) which indicates that the international access code needs to be dialed before dialing the number. If you are in North America and your phone number is 416-555-1212, then the value of this variable should be “+1 416 555 1212”.

  > **Note**
  > 
  > Notice the quotation marks around the value that are necessary because of the spaces in the value.

- **NAME**: Your name as it should appear on the header of outgoing faxes. You should put quotation marks around the name if it contains any spaces.
- **PAGE**: Your preferred page size. Possible values are `letter`, `legal` and `a4`. `a4` is the typical letter size sheet outside North America.
- **PRTYPE**: Your printer type. Generally, you should choose `ps` or `pcl` depending on whether you have a PostScript or Hewlett-Packard PCL-compatible printer. This setting governs how Efax will print received faxes.
