You can keep a count of how many times this memory-leaking application has serviced requests and kill it by programming around it. Listing 14-1 shows a simple example of how request-processing count is kept in a simple C-based FastCGI application. As the listing shows, when the maximum number of requests have been processed the FastCGI application exits.

```
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
            exit 0;
        }

        /* end of body code */
    }

    /* termination or clean-up code (if any) */
    exit(0);
}
```

```

# Migrating a sample script

This section demonstrates how to migrate `fontsize.cgi`, a simple CGI script (written in Perl), which is listed in Listing 14-2.