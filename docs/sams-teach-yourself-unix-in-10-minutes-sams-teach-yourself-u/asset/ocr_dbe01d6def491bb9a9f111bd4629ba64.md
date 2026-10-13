Subject: Re: Q: Booting lockup? How to solve?
Date: 3 Mar 1996 18:23:32 GMT
Organization: Northwestern University, Evanston, IL, US
Lines: 44
Message-ID: <4hc034s026@news.acns.nwu.edu>

In this example, the first ten lines of the file news112.msg are displayed. If you'd like to change the number of lines that are displayed, use the option -#, where # is the number of lines you'd like to view.

# VIEWING THE END: tail

Tail is the inverse of head. Instead of displaying files from the start of a file, tail shows what is at the end of a file. Because most logs grow by adding things to the end, tail is a very nice way to see the latest additions to any log.

For example

```
>tail /var/log/httpd/access_log
204.123.9.20 - - [28/Nov/1998:00:52:40 -0500] "GET
/../lifetime/lt2-1e.html HTTP/1.0" 200 3399
204.123.9.20 - - [28/Nov/1998:00:52:40 -0500] "GET
/../lifetime/lt1-2a.html HTTP/1.0" 200 3561
204.123.9.20 - - [28/Nov/1998:00:52:41 -0500] "GET
/../enviro/fa97/enviro_5.html HTTP/1.0" 200 3839
204.123.9.20 - - [28/Nov/1998:00:52:41 -0500] "GET
/../enviro/fa97/enviro_4.html HTTP/1.0" 200 3972
204.123.9.20 - - [28/Nov/1998:00:52:42 -0500] "GET
/../b865/b865_01.html HTTP/1.0" 200 15368
204.123.9.20 - - [28/Nov/1998:00:52:42 -0500] "GET
/../agf-fact/agf-125.html HTTP/1.0" 200 13540
204.123.9.20 - - [28/Nov/1998:00:52:43 -0500] "GET
/../aex-fact/463.html HTTP/1.0" 404 170
204.123.9.20 - - [28/Nov/1998:00:52:43 -0500] "GET
/../aex-fact/480_76.html HTTP/1.0" 404 173
204.123.9.20 - - [28/Nov/1998:00:52:43 -0500] "GET
/../hyg-fact/3000/3019.html HTTP/1.0" 200 8127
216.106.18.176 - - [28/Nov/1998:00:52:55 -0500] "GET
/../HTTP/1.1" 200 15679
```

The last ten entries from the Web server log are displayed. Because the log file is around 50MB in size, it's a good thing you don't have to read through it with cat or more just to see what's at the bottom! You can change the number of lines that tail displays by using the -# option just as you do with head.