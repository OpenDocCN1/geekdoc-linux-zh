# UNIX SYSTEM MANAGEMENT PRIMER PLUS

# Let Third Parties Know That You Are Monitoring Them

If you decide to use third-party data in your monitoring processes, as in the Yahoo! DNS example in this section, let the third party know that you are using their data. They may be able to alert you to changes ahead of time. This is most effective with organizations that you already have relationships with, such as your ISP or a parent company.

When indirectly monitoring third-party services as in the previous example, you also run the risk of experiencing false alarms as a result of the services becoming unavailable. This is an acceptable risk, if it happens more than a few times, your monitor query a different address or give it a series of addresses in a loop to avoid a single point of failure. You can read more about these third-party outages in Chapter 8.

# Timeouts and Repeats

The monitoring processes you've learned to this point in the chapter have tested services and passed or failed those services based on their responses to the tests. What if the services take 2 hours to respond, or what if they don't respond? Your monitoring tools should have the ability to timeout after a designated interval, at which point the test considers the service to be down.

There are no established rules for timeout values; the length of the timeout interval is highly dependent on the nature of each service. DNS, which drives the name-to-address translation that the Internet more user friendly, needs to be very responsive, so a timeout of 15 seconds is reasonable. SMTP, on the other hand, is not as time-sensitive as DNS, and is also more prone to sluggishness due to server load. An additional 20 seconds over the usual time to send an email is unimportant, so perhaps a timeout of 30 seconds is more appropriate for an SMTP service check.

Occasionally, a timeout is a fluke; nearly every Internet user has clicked on a link in a browser to wait two minutes for a DNS query to complete. These timeouts can be caused by network congestion or a quick burst of server activity—pinning down the cause can be difficult. In any case, most services shouldn't marked down because of a single timeout; a service test shortly after the first may yield a successful result. If a service fails the second test, the service should probably be marked down. Not all monitoring systems offer repeat testing, but if yours, you should definitely take advantage of it.

# Logging

System logs are a system administrator's best friend. They tell the story of each system, service, and network in your infrastructure. There are many types of logs, and each operating system and application has a different way of logging information. The most common manifestation of logs in Unix is the log file. This is a simple text file to which application or system log messages are appended. Well-constructed logs contain the date and time each message was