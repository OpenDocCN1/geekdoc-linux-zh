
# Solving the Quote Service Problem

![](img/961a0296fe36074690a9847b79332eff_492_0.png)

*Figure 18.1: A screen shot of Netscape after obtaining a stock quote for RHAT at* `http://finance.yahoo.com.`

From here, you have three choices:

- Move the mouse over the Download Spreadsheet Format link and note the URL that shows up on the status line (Netscape 4.7 shows the link URL there).

- Select from the menu item View->Page Source. Look through the HTML code for the link that looks something like `<a href="/d/quotes.csv?ts=RHAT&f=s!1d1tclc1oghwg&f=.csv">Download Spreadsheet Format</a>` (find it by looking for *Download Spreadsheet Format*).

- The best way this information can be captured with Netscape is to right-click on the Download Spreadsheet Format link. From the pop-up menu, select the item Copy Link Location. This will copy the link reference to your Clipboard. Then, you can later paste this information into a file.

## Chapter 18: A Practical Network Project

From this information, you will have all that you need. Test the facility with telnet as follows (remember to supply 80 after the hostname):

```
$ telnet finance.yahoo.com 80
Trying 204.71.201.75...
Connected to finance.yahoo.com.
Escape character is '^]'.
GET /dq/quotes.csv?s=RHAT&f=ss11d1tc1of9hq&a=.csv
"RHAT",168.9375,'11/24/1999','4:00PM',0,147.5625,175.5,145.6875,3661700
Connection closed by foreign host.
$
```

![](img/961a0296fe36074690a9847b79332eff_493_0.png)

The GET command is issued after you are connected, along with the strange-looking pathname and a press of the Enter key (you might need to press Enter twice). If you are successful, you get one line of spreadsheet data in return! Substituting another symbol for RHAT will yield different data.

If you are not having any luck, then check your punctuation and spelling. Accuracy is vital here. Use cut and paste from the screen if possible. If this doesn't help, then you'll need to research how finance.yahoo.com is doing it presently (you might even need to start at the yahoo.com home page). Follow the steps outlined previously so that you'll be able to find out the new hostname and pathname required.

This is a summary of the quote fetch procedure:

1. Connect to finance.yahoo.com on port 80 (this hostname might change at a future date).
2. Issue the GET request with the magic pathname shown (the word GET should be uppercase).
3. A line of spreadsheet format data is returned on the same socket as a response.
4. The socket is closed.

That is all there is to it! Remember these steps when you examine the source code listings later.

The following sections will illustrate and describe the modules that make up the server and client programs. Unfortunately, space does not permit a full listing of the source code. The full source code and make files are available, however, at http://www.quecorp.com/series/by_example/.

Table 18.1 lists all the source files that you will need. Some of the more interesting ones will be listed and described within this chapter.

### Table 18.1: Source Modules for the Quote Server and Client

| Source File | Description |
|---|---|
| Makefile | The project make file. |
| bcast.c | Implements the function that performs the quote broadcasting to the local area network. |
| connect.c | Implements a function that connects to the remote Internet quote server. |
| csparse.c | Parser for the quote data that is returned... |
| getick.c | Fetches the quote information from the remote Internet quote server. |
| load.c | Loads the stock market ticker symbols from file tickers.rc. |
| misc.c | Small miscellaneous functions. |
| mkaddr.c | The Internet address convenience function. |
| mktwatch.c | The market watch client program. This program receives the local broadcast information and displays it. |
| msgf.c | A module that logs server messages to the syslog logging facility. |
| qserve.c | The module that implements the local quote server program. |
| quotes.h | The common header file for all source modules. |
| tickers.rc | The list of ticker symbols to inquire about. Modify this file to change the tickers to the ones that interest you. |

## Examining the Quote Server Program

The logical place to start examining code is the qserve.c source module. This module forms the main program for the quote server itself. It is responsible for obtaining stock market quotes and then broadcasting them to the local area network. Listing 18.1 shows the source listing for qserve.c.

### Listing 18.1: qserve.c—The Quote Server Module

```c
/* qserve.c:
 *
 * Stock Quote Concentrator Program:
 */
#include "quotes.h"

static char *command = NULL;

/* Remote Quote Server Address */
static char *cmdopt_a = DFLT_SERVER;

/* Quote Re-Broadcast Address */
static char *cmdopt_b = DFLT_BCAST;

/* Ticker Table: */
static TickReq tickers[MAX_TICKERS];
static int ntick = 0;

/* Return server usage information: */
static void
usage(void) {
    printf("Usage: %s [-h] -a address:port\n"
           "where:\n"
           "\t-t\tRequests usage info,\n"
           "\t-a address:port\tSpecify "
           "the server\n"
           "\t\taddress and port number.\n"
           "\t-b bcast:port\tSpecify "
           "the broadcast\n"
           "\t\taddress and port number.\n",
           command);
}

/* Server Main Program: */
int
main(int argc, char **argv) {
    int rc = 0; /* Return Code */
    int optch;  /* Option Char. */
    int z;      /* Status Code */
    int x;      /* Index */
    int s;      /* Broadcast socket */
    time_t tn = 0; /* Time Next */
    time_t tzz;   /* Sleep Time */
    time_t tm = 20; /* Seconds */
    time_t td;    /* Time + Date */
    struct sockaddr_in bc_addr; /* bc addr */
    socklen_t bc_len; /* bc addr len. */
    const int True = TRUE; /* Const. TRUE */
    static char cmdopts[] = "ha:b:";

    /* Process command line options: */
    command = Basename(argv[0]);

    while ( (optch = getopt(argc, argv, cmdopts)) != -1 )
        switch ( optch ) {
        case 'h' :               /* -h for help */
            usage();
            return rc;

        case 'a' :               /* -a quote_server */
            cmdopt_a = optarg;
            break;

        case 'b' :   /* -b broadcast_addr */
            cmdopt_b = optarg;
            break;

        default :
            /* Option error */
            rc = 1;
        }

        /*
         * Check for option errors:
         */
        if ( rc ) {
            usage();
            return rc;
        }

        /*
         * Form the broadcast server
         * address:
         */
        bc_len = sizeof bc_addr;   /* Max len */
        z = mkaddr(
                &bc_addr,        /* Returned addr. */
                &bc_len,        /* Returned len. */
                cmdopt_b,       /* Input address */
                "udp" );        /* UDP protocol */

        if ( z == -1 ) {
            msgf("e", "%s: -b %s", 
                 strerror(errno),
                 cmdopt_b);
            return 1;
        }

        /*
         * Create a UDP socket to use:
         */
        s = socket(AF_INET, SOCK_DGRAM, 0);

        if ( s == -1 ) {
            msgf('e', "s: socket(AF_INET, "
                 "SOCK_DGRAM,0)",
                 strerror(errno));
            return 1;
        }

        /*
         * Allow broadcasts on socket s:
         */
        z = setsockopt(s,
                 SOL_SOCKET,
                 SO_BROADCAST,
                 &True,
                 sizeof True);

        if ( z == -1 ) {
            msgf('e', "s: setsockopt(SO_BROADCAST)",
                 strerror(errno));
            return 1;
        }

        /*
         * Load tickers from tickers.rc:
         */
        if ( load(&tickers[0], &ntick, MAX_TICKERS) )
            goto errxit;

        /*
         * Now monitor the remote quote server:
         */
        for (;;) {
            tn = 0;                /* Refresh tn */
            time(&td);            /* Current time */

            /*
             * Loop for all tickers:
             */
            for ( x=0; x<ntick; ++x ) {
                /*
                 * Get quote for ticker x
                 */
            }
        }
    }
}
```
