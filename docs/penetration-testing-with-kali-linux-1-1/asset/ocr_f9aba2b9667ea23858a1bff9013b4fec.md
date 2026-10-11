```
report_wget.pdf

100%[==>===========================>] 26.41M 766KB/s in 28s

2018-01-28 20:38:33 (964 KB/s) - 'report_wget.pdf' saved [27691955/27691955]

Listing 67 - Downloading a file through wget
```

# 3.8.2 curl

curl<sup>78</sup> is a tool to transfer data to or from a server using a host of protocols including IMAP/S, POP3/S, SCP, SFTP, SMB/S, SMTP/S, TELNET, TFTP, and others. A penetration tester can use this to download or upload files and build complex requests. Its most basic use is very similar to wget, as shown in Listing 68:

```
kali@kali:~$ curl -o report.pdf https://www.offensive-security.com/reports/pentration -testing-sample-report-2013.pdf

% Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                              Dload  Upload   Total   Spent    Left  Speed

  100  26.4M    100  26.4M      0      0    1590k      0  0:00:17  0:00:17 --:--:--   870k

Listing 68 - Downloading a file with curl
```

# 3.8.3 axel

axel<sup>79</sup> is a download accelerator that transfers a file from a FTP or HTTP server through multiple connections. This tool has a vast array of features, but the most common is *-n*, which is used to specify the number of multiple connections to use. In the following example, we are also using the *-a* option for a more concise progress indicator and *-o* to specify a different file name for the downloaded file.

```
kali@kali:~$ axel -a -n 20 -o report_axel.pdf https://www.offensive-security.com/repor ts/pentration-testing-sample-report-2013.pdf

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
```

<sup>78</sup> (MIT, 2004), http://www.mit.edu/afs/new/sipb/user/ssern/src/curl-7.11.1/docs/curl.html
<sup>79</sup> (Ubuntu, 2019), http://manpages.ubuntu.com/manpages/xenial/man1/axel.1.html