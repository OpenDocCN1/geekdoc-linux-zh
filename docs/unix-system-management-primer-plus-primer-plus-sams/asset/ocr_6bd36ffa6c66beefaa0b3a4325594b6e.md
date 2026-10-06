numeric pager communications more tolerable, numeric pagers usually aren't the right solution for a notification system.

Text pagers can receive text messages of several kilobytes and have larger displays that can display several lines of each message at a time. Messages can be sent to pagers by an operator at a dispatch center, through a modem, or through email. Many modern text pagers are two-way and can both receive and send messages. Text pagers are clearly the notification tool of choice for any system administrator.

Email and modem are the two most popular methods of sending pages. Although email is highly convenient and integrates into all monitoring systems, or your email infrastructure must be operational in order for you to send email messages. If your email servers are down, you can't receive a notification of the problem via email.

Out-of-band communication solves this problem. Using infrastructure that is outside your production network guarantees that pages will be sent out even if your system has lost connectivity to the Internet. Modem falls into this out-of-band category, and most pager services today provide a modem gateway to your pager. These services usually provide a public phone number through which anybody can send pages TAP (Telocator Alphanumeric Protocol, also known as the IXO protocol). Using a modem attached to your monitoring server to send pages completely separates your infrastructure from your notification mechanisms; you'll never be in the dark when something goes down.

# Monitor Your Monitoring Server

It is important to keep watch over your monitoring server so it is always available to notify you in case of failures. A simple ping test from a separate server can alert you when your monitoring server crashes (this is covered in the "Network Monitoring" section of this chapter).

Several paging software packages are available on Unix, but by far the most versatile and cost-effective (free) Qpage (http://www.qpage.org). Although it's been three years since the last release, Qpage enjoys widespread use, and it's still a good example of what to look for in paging software:

+   - Support for TAP/IXO.
- Client-server architecture; paging clients can send pages through multiple servers in a failover fashion, providing redundancy.
- Pager groups facilitate sending pages to multiple users using one identifier.
- Message queues store messages for periodic transmissions and during retries.

# Cell Phones

Cell phones are becoming an increasingly popular notification mechanism, as prices for both service and phones decrease and wireless features increase. Conventionally, cell phones have been used as a secondary notification mechanism when pagers didn't work. Today, in addition