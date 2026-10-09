
**Filters:** You can create a FastCGI filter application to process a requested file before it is returned to the client. For example, say you want to apply a standard set of headers and footers for each HTML (.html) page returned by the Web server. This is possible using a FastCGI filter application. When a request for an .html file comes to the server, it sends the file request to the FastCGI filter responsible for adding the header and footer. The FastCGI application returns the resulting HTML page to the server, which, in turn, is transmitted to the client.

FastCGI filter applications can significantly improve performance by caching filter results (the server provides the modification time in the request information so that applications can flush the cache when the server file has been modified). Filter applications are useful in developing parsers for HTML pages with embedded SQL statements, on-the-fly file format converters, and so on.

**External authentication applications:** Other new types of applications that can be developed using FastCGI support include external authentication programs and gateways to third-party authentication applications. For example, if you use an external database server to store authentication information such as username, passwords, or other permission-specific data, you can create a FastCGI application to keep a persistent connection to the database server and to perform queries to authenticate access requests. Can this be done with a CGI application? Yes, except that a CGI application has to open the connection to the database server each time it is run. This could become expensive in terms of resource (CPU, network) utilization.

On the other hand, the FastCGI version of the same application maintains a single connection to the database server, performs queries, and returns appropriate HTTP status code based on the results of the queries. For example, when an access request is accompanied with a valid username/password pair, the FastCGI application queries the database server to determine whether the pair is allowed access to the requested resource. If the database server returns a specific value indicating that access should be allowed, the FastCGI application returns a 200 OK HTTP status code; when authorization fails, it can send a different HTTP status code, such as 401 Unauthorized.

## Migrating from CGI to FastCGI

One of the main advantages of FastCGI is that the migration path from CGI to FastCGI is reasonably simple. Special Perl-based CGI scripts that use CGI.pm module can easily be turned into FastCGI applications. Any CGI program written in other languages such as C, C++, Tcl, or Java can also be converted using the FastCGI Software Development Kit (SDK).

![](img/e11fcbd2818a3495ac70085e5d8d1c26_439_0.png)

The developers of FastCGI specifications provides a freely available software development kit (SDK) to help ease the process of FastCGI application development. The SDK is also included on the CD-ROM. This kit, provided as a compressed tar file, helps you to write FastCGI applications in C, C++, Perl, Tcl, and Java. When you uncompress and extract the tar file, it creates a fcgi-dev-kit directory. An index.html file provides information on what is available in the kit. The kit can also be obtained from the FastCGI Web site at www.fastcgi.com/applibs.

## Things to keep in mind about migrating

The following list gives you a few tips to keep in mind when migrating CGI applications:

- Another issue to be aware of is this: If the CGI application being migrated has code that might interfere with a second run of the body code, it has to be fixed. The solution to this problem could be as simple as adding code to reinitialize some variables, arrays, and so on. The application must ensure that any state it creates in processing one request has no unintended effect on later requests.

- It’s a common practice among CGI developers to subdivide a large application into smaller CGI applets, as a way to compensate for the initialization penalty associated with CGI applications. With FastCGI, it’s better to have related functionality in a single executable so that there are fewer processes to manage and applications can take advantage of sharing cached information across functions.

- To ease migration to FastCGI, executables built with the FCGI module can run as either CGI or FastCGI programs, depending on how they are invoked. The module detects the execution environment and automatically selects FastCGI or regular I/O routines, as appropriate.

- Many CGI applications are written so that they do not attempt to perform any memory management operations. This is a consequence of CGI applications exiting after execution, and in most cases, the operating system is able to restore memory for other use. On top of that, many CGI applications do not even attempt to close files, as the responsibility is handed over to the operating system at exit.

In such a case, it is very important that these types of applications be fixed while migrating to the FastCGI version. Remember that FastCGI applications reside in memory as long as the Web server or the administrator does not kill them. If a CGI application that leaked memory is converted to FastCGI without anyone dealing with the memory issue, the FastCGI version might leak memory over time, eventually causing a resource fault. Avoid long weekends in the office by looking at this issue beforehand. If the CGI application is very complex, and fixing it to behave nicely (memory usage-wise) is too expensive in terms of time and effort, another solution is available to you.

You can keep a count of how many times this memory-leaking application has serviced requests and kill it by programming around it. Listing 14-1 shows a simple example of how request-processing count is kept in a simple C-based FastCGI application. As the listing shows, when the maximum number of requests have been processed the FastCGI application exits.

**Listing 14-1: memory\_hog.c**

```c
#include <fcgi_stdio.h>
void main(void){
    int maxRequests = 100;         // maximum num of request
    before exiting.
    int requestCount = 0;          // used to keep count of
    requests processed so far.

    while(FCGI_Accept() >= 0) {    // start of response loop
        /* body code */

        printf("Content-type: text/html\r\n");
        printf("\r\n");
        printf("Number of requests processed so far is %d.", requestCount++);

        /* some memory leaking code could go here */

        /* end of application code */

        if(requestCount >= maxRequests) {
            /* clean-up code goes here */
            exit(0);
        }

        /* end of body code */
    }

    /* termination or clean-up code (if any) */
    exit(0);
}
```

## Migrating a sample script

This section demonstrates how to migrate `fontsize.cgi`, a simple CGI script (written in Perl), which is listed in Listing 14-2.

**Listing 14-2: fontsize.cgi**

```perl
#!/usr/bin/perl  -w

# Variables
my $MAX = 10;
my $i;

# Content Header
print "Content-type: text/html\n\n";

# Main loop
for ($i=0; $i < $MAX; $i++){

    print "<FONT SIZE=$i>Font Size = $i</FONT><BR>";
}

exit 0;
```

This CGI application produces the output shown in Figure 14-5.

![](img/e11fcbd2818a3495ac70085e5d8d1c26_441_0.png)

**Figure 14-5:** Output of the `fontsize.cgi` script

Now let’s convert this to a FastCGI application. First you need to make sure you have installed the FCGI module from a Comprehensive Perl Archive Network (CPAN) site by following these steps:

1. As `root`, from the command-line run the following command:
   ```perl
   perl -MCPAN -e shell
   ```

2. At the `cpan>` prompt enter the `install FCGI` command, which will install the latest version of this CPAN module if you do not already have the latest.

3. As the second line in the above script, add the following line:
   ```perl
   use FCGI;
   ```
   This tells Perl to load the FCGI module when running the script.

4. Identify the initialization block of the CGI application. For this script the initialization block consists of the following two variable declarations:
   ```perl
   my $MAX = 10;
   my $i;
   ```

5. Identify the response loop and body blocks of the CGI application. Because every request must be responded to with an appropriate Content-Type header, the body of the main code begins with this line:
   ```perl
   print "Content-type: text/html\n\n";
   ```
   The for loop responsible for the actual processing is the rest of the body.

6. Now that the body code is identified, you need to put the response loop around it. This is done using the following code:
   ```perl
   while(FCGI::accept() >= 0) {
   # body code goes here
   }
   ```
   Now the body looks like this:
   ```perl
   while(FCGI::accept() >= 0) {
   print "Content-type: text/html\n\n";

   for ($i=0; $i < $MAX; $i++){
   print "<FONT SIZE=$i>Font Size = $i</FONT><BR>";
   }
   }
   ```

FastCGI applications act like server applications, so the following line is only executed if the Web server or the administrator sends the application a signal to terminate:
```perl
exit 0;
```

The FastCGI version of the entire application is listed in Listing 14-3.
