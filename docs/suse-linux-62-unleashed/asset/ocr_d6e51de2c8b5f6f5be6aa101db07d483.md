# Networking and Internet Services
PART II

SMTP client uses to communicate with the SMTP server. The text following the reply
codes is only for human consumption.

Although this dialog still might look a little mysterious, it will soon be very familiar if you
take the time to read RFC 821. Running sendmail with its -v option will also help you
understand how an SMTP dialog works.

# The Domain Name System and Email

Names like whizzer.com are convenient for humans, but computers insist on using
umerical IP addresses like 123.45.67.1. The Domain Name Service (DNS) provides this
hostname-to-IP address translation and other important information.

In the old days (when most of us walked several miles to school through deep snow), only a
thousand hosts were on the Internet. All hosts were registered with the Network
Information Center (NIC), which distributed a host table listing the hostnames and IP
addresses of all the hosts on the Internet. Those times are gone forever. No one
really knows how many hosts are connected to the Internet now, but they number in the
millions. It is physically impossible for an administrative entity such as the NIC to keep
track of every Internet address. This was born due.

The DNS distributes the authority for naming and hosting to autonomous
administrative domains. For example, a company called whizzer.com can maintain all the
information about the hosts in its own domain. When the host a.whizzer.com wants to
s mail or telnet to the host b.whizzer.com, it sends an inquiry over the network to the
whizzer.com nameserver, which might run on a host named ns.whizzer.com. The
ns.whizzer.com nameserver replies to a.whizzer.com with the IP address of b.whiz-
zer.com (and possibly other information), and the mail is sent or the telnet connection
made. Because ns.whizzer.com is authoritative for the whizzer.com domain, it can
answer any inquiries about whizzer.com regardless of where they originate.
The authority for naming hosts in this domain has been delegated.

Now, if someone on a.whizzer.com wants to send mail to joe@gonzo.gov?
ns.whizzer.com has no information about hosts in gonzo.gov domain, but it knows
how to find this information. When a nameserver receives a request for a host in a domain
for it has no information, it asks the root nameservers for the names and IP addresses
of servers that are authoritative for that domain—in this case, gonzo.gov. The root
nameserver gives the ns.whizzer.com nameserver the names and IP addresses of hosts
running nameservers with authority for gonzo.gov. The ns.whizzer.com nameserver
inquires of them and forwards the reply to a.whizzer.com.