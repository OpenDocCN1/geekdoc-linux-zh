```
09:    *)              SENDTO="FaxSec@bwc.org" ;;
10: esac
```

The script is quite simple. It is invoked from within the /var/spool/fax/bin/faxrcvd script. It can be analyzed as follows:

+   - Lines 1-5 are comment lines.
+   - Lines 6-10 are part of one case statement. The case statement matches each TSI against well-known ones. If a match is found, the SENDTO variable is assigned the designated user’s email address. At the end we have a default case that matches everything that did not match earlier. These fax messages are sent to an individual who serves as a fax processor and prints and distributes hard copies to the recipients.

HylaFAX currently does not support the Direct Inward Dial (DID) service, because the DID hardware devices use non-standard programming interfaces. In the future, when updated versions of the ITU facsimile protocols are supported in commercial fax modems HylaFAX will be able to use routing information provided in the protocol to do automatic delivery of inbound facsimile.

# HylaFAX Client Setup

So far everything you have done was on the Fax Server machine. Now it is time to setup a fax client machine and make sure you can send faxes from it using the HylaFAX server.

HylaFAX uses a client/server architecture. A single server is capable of servicing several network client machines. Client and server machines communicate with each other using a special HylaFAX protocol that runs on top of the TCP/IP protocols. Clients can also use other methods of submitting fax jobs to the server, such as email. Email-fax gateways are discussed in the next section.

A client machine will require the following programs be installed in the /usr/bin directory:

+   - `sendfax`
+   - `sendpage`
+   - `faxstat`
+   - `faxrm`
+   - `faxalter`
+   - `fax2ps`

In addition, the following configuration and supporting files are needed in the /usr/share/fax directory:

+   - `afm`
+   - `faxcover.ps`
+   - `faxmail.ps`
+   - `hfaxd.conf`