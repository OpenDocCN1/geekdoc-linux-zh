```
kali@kali:~$ wc -l access.log
1173 access.log
```

*Listing 48 - Peeking into the access.log file to understand its structure*

Notice that the log file is text-based and contains different fields (IP address, timestamp, HTTP request, etc.) that are delimited by spaces. This is a perfectly "*grep friendly*" file and will work well for all of the tools we have covered so far. We'll begin by searching through the HTTP requests made to the server for all the IP addresses recorded in this log file. We'll do this by piping the output of the **cat** command into the **cut** and **sort** commands. This may give us a clue about the number of potential attackers we will need to deal with.

```
kali@kali:~$ cat access.log | cut -d " " -f 1 | sort -u
201.21.152.44
208.115.113.91
208.54.80.244
208.68.234.99
70.194.129.34
72.133.47.242
88.112.192.2
98.238.13.253
99.127.177.95
```

*Listing 49 - Piping commands in order to get required information from the file*

We see that less than ten IP addresses were recorded in the log file, although this still doesn't tell us anything about the attackers. Next, we use **uniq** and **sort** to show unique lines, further refine our output, and sort the data by the number of times each IP address accessed the server. The **-c** option of **uniq** will prefix the output line with the number of occurrences.

```
kali@kali:~$ cat access.log | cut -d " " -f 1 | sort | uniq -c | sort -urn
     1038 208.68.234.99
       59 208.115.113.91
       22 208.54.80.244
       21 99.127.177.95
        8 70.194.129.34
        1 201.21.152.44
```

*Listing 50 - Using the uniq command to get a count per IP address in the file*

A few IP addresses stand out but we will focus on the address that has the highest access frequency first. To filter out the 208.68.234.99 address and display and count the resources that were being requested by that IP, we can use the following sequence:

```
kali@kali:~$ cat access.log | grep '208.68.234.99' | cut -d """ -f 2 | uniq -c
     1038 GET //admin HTTP/1.1
```

*Listing 51 - Exploring the resources accessed by a specific IP address*

From this output, it seems that the IP address at 208.68.234.99 was accessing the /admin directory exclusively. Let's inspect this further.

```
kali@kali:~$ cat access.log | grep '208.68.234.99' | grep '/admin ' | sort -u
208.68.234.99 - - [22/Apr/2013:07:51:20 -0500] "GET //admin HTTP/1.1" 401 742 "-" "Teh Forenst Lobster"
208.68.234.99 - admin [22/Apr/2013:07:51:25 -0500] "GET //admin HTTP/1.1" 200 575 "-"
```