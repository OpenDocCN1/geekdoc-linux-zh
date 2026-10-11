
## 3.6.2 Managing Processes
(Implied context from "use kill...")
To use **kill**, we need the PID of the process we want to send the signal to. Since we gathered Leafpad's PID in the previous step, we can proceed:

```bash
kali@kali:~$ kill 1397

kali@kali:~$ ps aux | grep leafpad
kali 1313 0.0 0.0 6144 888 pts/0 S+ 10:59 0:00 grep leafpad
```

![](img/ec25e59d75726b7041242a56d3376832_68_0.png)

Because the default signal for `kill` is *SIGTERM* (request termination), our application has been terminated. This has been verified in Listing 64 by using **ps** after killing Leafpad.

### 3.6.3.1 Exercises

- 1. Find files that have changed on your Kali virtual machine within the past 7 days by running a specific command in the background.
- 2. Re-run the previous command and suspend it; once suspended, background it.
- 3. Bring the previous background job into the foreground.
- 4. Start the Firefox browser on your Kali system. Use **ps** and **grep** to identify Firefox's PID.
- 5. Terminate Firefox from the command line using its PID.

## 3.7 File and Command Monitoring

It is extremely valuable to know how to monitor files and commands in real-time during the course of a penetration test. Two commands that help with such tasks are *tail* and *watch*.

### 3.7.1 tail

The most common use of `tail`<sup>75</sup> is to monitor log file entries as they are being written. For example, we may want to monitor the Apache logs to see if a web server is being contacted by a given client we are attempting to attack via a client-side exploit. This example will do just that:

```bash
kali@kali:~$ sudo tail -f /var/log/apache2/access.log

127.0.0.1 - - [02/Feb/2018:12:18:14 -0500] "GET / HTTP/1.1" 200 3380 "-" "Mozilla/5.0 (X11; Linux x86_64; rv:52.0) Gecko/20100101 Firefox/52.0"
127.0.0.1 - - [02/Feb/2018:12:18:14 -0500] "GET /icons/openlogo-75.png HTTP/1.1" 200 6040 "http://127.0.0.1/" "Mozilla/5.0 (X11; Linux x86_64; rv:52.0) Gecko/20100101 Firefox/52.0"
127.0.0.1 - - [02/Feb/2018:12:18:15 -0500] "GET /favicon.ico HTTP/1.1" 404 500 "-" "Mozilla/5.0 (X11; Linux x86_64; rv:52.0) Gecko/20100101 Firefox/52.0"
```

![](img/ec25e59d75726b7041242a56d3376832_68_1.png)

The **-f** option (follow) is very useful as it continuously updates the output as the target file grows. Another convenient switch is **-nX**, which outputs the last "X" number of lines, instead of the default value of 10.

### 3.7.2 watch

The `watch`<sup>76</sup> command is used to run a designated command at regular intervals. By default, it runs every two seconds, but we can specify a different interval by using the `--interval` (`-n X`) option to have it run every "X" number of seconds. For example, this command will list logged-in users (via the `w` command) once every 5 seconds:

```bash
kali@kali:~$ watch -n 5 w

Every 5.0s: w                                kali: Tue Jan 23 21:06:03 2018

21:06:03 up 7 days, 3:54,  1 user,  load average: 0.18, 0.09, 0.03
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU  WHAT
kali     tty2     :0               16Jan18  7days  16:29  2.51s /usr/bin/python
```

> *Listing 66 - Monitoring logged in users using the watch command.*

To terminate the `watch` command and return to the interactive terminal, use `Ctrl C`.

#### 3.7.2.1 Exercises

- 1. Start your apache2 web service and access it locally while monitoring its `access.log` file in real-time.
- 2. Use a combination of `watch` and `ps` to monitor the most CPU-intensive processes on your Kali machine in a terminal window; launch different applications to see how the list changes in real time.

## 3.8 Downloading Files

Next, let's take a look at some tools that can download files to a Linux system from the command line.

### 3.8.1 wget

The `wget`<sup>77</sup> command, which we will use extensively, downloads files using the HTTP/HTTPS and FTP protocols. Listing 67 shows the use of `wget` along with the `-O` switch to save the destination file with a different name on the local machine:

```bash
kali@kali:~$ wget -O report_wget.pdf https://www.offensive-security.com/reports/pentration-testing-sample-report-2018.pdf
--2018-01-28 20:30:04--  https://www.offensive-security.com/reports/pentration-testing-sample-report-2018.pdf
Resolving www.offensive-security.com (www.offensive-security.com)... 192.124.249.5
Connecting to www.offensive-security.com (www.offensive-security.com)|192.124.249.5|:4
HTTP request sent, awaiting response... 200 OK
Length: 27691955 (26M) [application/pdf]
Saving to: 'report_wget.pdf'

100%[==>===========================>] 26.41M 766KB/s in 28s

2018-01-28 20:38:33 (964 KB/s) - 'report_wget.pdf' saved [27691955/27691955]
```

> *Listing 67 - Downloading a file through wget*

### 3.8.2 curl

`curl`<sup>78</sup> is a tool to transfer data to or from a server using a host of protocols including IMAP/S, POP3/S, SCP, SFTP, SMB/S, SMTP/S, TELNET, TFTP, and others. A penetration tester can use this to download or upload files and build complex requests. Its most basic use is very similar to `wget`, as shown in Listing 68:

```bash
kali@kali:~$ curl -o report.pdf https://www.offensive-security.com/reports/pentration-testing-sample-report-2013.pdf

% Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                              Dload  Upload   Total   Spent    Left  Speed

  100  26.4M    100  26.4M      0      0    1590k      0  0:00:17  0:00:17 --:--:--   870k
```

> *Listing 68 - Downloading a file with curl*

### 3.8.3 axel

`axel`<sup>79</sup> is a download accelerator that transfers a file from a FTP or HTTP server through multiple connections. This tool has a vast array of features, but the most common is *-n*, which is used to specify the number of multiple connections to use. In the following example, we are also using the *-a* option for a more concise progress indicator and *-o* to specify a different file name for the downloaded file.

```bash
kali@kali:~$ axel -a -n 20 -o report_axel.pdf https://www.offensive-security.com/reports/pentration-testing-sample-report-2013.pdf

Initializing download: https://www.offensive-security.com/reports/pentration-testing - File size: 27691955 bytes

Opening output file report_axel.pdf

Starting download

Connection 0 finished
Connection 1 finished
Connection 2 finished
Connection 3 finished
Connection 4 finished
Connection 5 finished
Connection 6 finished
Connection 7 finished
Connection 8 finished
Connection 9 finished
Connection 10 finished
Connection 11 finished
Connection 13 finished
Connection 14 finished
Connection 15 finished
Connection 16 finished
Connection 18 finished
[100%]  
[  11.1MB/s] [00:00]

Downloaded 26.4 Megabyte in 2 seconds. (11380.17 KB/s)
```

### 3.8.3.1 Exercise

- 1. Download the PoC code for an exploit from https://www.exploit-db.com using **curl**, **wget**, and **axel**, saving each download with a different name.

## 3.9 Customizing the Bash Environment

### 3.9.1 Bash History Customization

Earlier in this module, we discussed environment variables and the history command. We can use a number of environment variables to change how the history command operates and returns data, the most common including HISTCONTROL, HISTIGNORE, and HISTTIMEFORMAT.

The HISTCONTROL variable defines whether or not to remove duplicate commands, commands that begin with spaces from the history, or both. By default, both are removed, but you may find it more useful to only omit duplicates.

```bash
kali@kali:~$ export HISTCONTROL=ignoredups
```

The HISTIGNORE variable is particularly useful for filtering out basic commands that are run frequently, such as `ls`, `exit`, `history`, `bg`, etc.

```bash
kali@kali:~$ export HISTIGNORE="&;ls:[bf]g;exit;history"

kali@kali:~$ mkdir test

kali@kali:~$ cd test

kali@kali:~/test$ ls

kali@kali:~/test$ pwd
/home/kali/test

kali@kali:~/test$ ls

kali@kali:~/test$ history
  1  export HISTIGNORE="&;ls:[bf]g;exit;history"
  2  mkdir test
  3  cd test
  4  pwd
```

Lastly, HISTTIMEFORMAT controls date and/or time stamps in the output of the **history** command.

[footnotes]
<sup>75</sup> tail command reference implied
<sup>76</sup> (die.net, 1999), https://linux.die.net/man/1/watch
<sup>77</sup> (GNU, 2018), https://www.gnu.org/software/wget/manual/wget.html
<sup>78</sup> (MIT, 2004), http://www.mit.edu/afs/new/sipb/user/ssern/src/curl-7.11.1/docs/curl.html
<sup>79</sup> (Ubuntu, 2019), http://manpages.ubuntu.com/manpages/xenial/man1/axel.1.html
