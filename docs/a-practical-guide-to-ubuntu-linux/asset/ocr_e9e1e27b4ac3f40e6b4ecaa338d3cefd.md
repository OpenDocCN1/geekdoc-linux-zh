# ADVANCED EXERCISES

+   1. Write a regular expression to match an IP address in a log file.

+   2. Many configuration files contain many comments, including commented-out default configuration directives. Write a program to remove these comments from a configuration file.

+   3. Write a program that removes ~ and *.ico files from a directory hierarchy (Hint: Use the File::Find module).

+   4. Describe a programming mistake that Perl's warnings do not report.

+   5. Write a program that counts the number of files in the directory and the number of bytes in those files, by filename extension.

+   6. Describe the difference between quoting strings using single quotation marks and using double quotation.

+   7. Write a program that copies all files with a *.ico extension in a directory hierarchy to a directory named in your home directory (Hint: Use the File::Find and File::Copy modules).

+   8. Write a program that analyzes Apache access logs. Display the number of bytes served by each path. Ignore unsuccessful page requests. If there are more than ten paths, display the first ten only.

Following is a sample line from Apache access log. The two numbers following the HTTP/1.1 are the response code and the byte count. A response code of 200 means the request was successful. A byte count of means no data was transferred.

```
_DATA_ [19/Aug/2008:08:26:43 -0400] "GET /perl/automated-testing/next_active.gif HTTP/1.1" 200 980 "http://example.com/perl/automated-testing/navigation_bar.htm"
"Mozilla/5.0 (X11; U; Linux x86_64; en-US; rv:1.8.1.6) Gecko/20061201 Firefox/3.0.0 (Fedora); Blazer/4.0"
```