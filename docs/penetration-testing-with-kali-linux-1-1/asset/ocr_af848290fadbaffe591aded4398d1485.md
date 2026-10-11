```
sys
sync
games
...

```

+   Listing 46 - Extracting usernames from /etc/passwd using cut

# 3.3.4 awk

AWK 59 is a programming language designed for text processing and is typically used as a data extraction and reporting tool. It is also extremely powerful and can be quite complex, so we will only scratch the surface here. A commonly used switch with awk 60 is -F, which is the field separator, and the print command, which outputs the result text.

```
kali@kali:~$ echo "hello:there:friend" | awk -F ":" '{print $1, $3}'
hello friend

```

+   Listing 47 - Extracting fields from a stream using a multi-character separator in awk

In Listing 47, we echoed a line and piped it to awk to extract the first ($1) and third ($3) fields using : as a field separator. The most prominent difference between the cut and awk examples we used is that cut can only accept a single character as a field delimiter, while awk, as shown in Listing 47, is much more flexible. As a general rule of thumb, when you start having a command involving multiple cut operations, you may want to consider switching to awk.

# 3.3.5 Practical Example

Let's take a look at a practical example that ties together many of the commands we have explored so far.

We are given an Apache HTTP server log (http://www.offensive-security.com/pwk-files/access_log.txt.gz), that contains evidence of an attack. Our task is to use Bash commands to inspect the file and discover various pieces of information, such as who the attackers were and what exactly happened on the server.

First, we'll use the head and wc commands to take a quick peek at the log file to understand its structure. The head command displays the first 10 lines in a file and the wc command, along with the -l option, displays the total number of lines in a file.

```
kali@kali:~$ gunzip access_log.txt.gz
kali@kali:~$ mv access_log.txt access.log

```

```
kali@kali:~$ head access.log
201.21.152.44 -- [25/Apr/2013:14:05:35 -0700] "GET /favicon.ico HTTP/1.1" 404 89 "-"
"Mozilla/5.0 (Windows NT 6.2; WOW64) AppleWebKit/537.31 (KHTML, like Gecko) Chrome/26.0.1410.64 Safari/537.31" "random-site.com"
70.194.129.34 -- [25/Apr/2013:14:10:48 -0700] "GET /include/jquery.jshowoff.min.js HTTP/1.1" 200 2553 "http://www.random-site.com/" "Mozilla/5.0 (Linux; U; Android 4.1.2; en-us; SCH-I535 Build/JZ054K) AppleWebKit/534.30 (KHTML, like Gecko) Version/4.0 Mobile Safari/534.30" "www.random-site.com"

```

+   59 (Wikipedia, 2019), https://en.wikipedia.org/wiki/AWK

+   60 (GNU, 2019), https://www.gnu.org/software/gawk/manual/gawk.html