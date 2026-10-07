# Chapter 11 Stopping Spam

37.72.168.192.dns1.foobirds.org. IN A 127.0.0.2
9.200.168.192.dns1.foobirds.org. IN A 127.0.0.2

NOTE To find out more about building a DNS zone file, see Linux Server Administration by Craig Hunt (Syybex, 2000).

Once the DNS zone has been created and a Sendmail configuration has been built using the correct dnsbl feature, the new configuration can be tested by running the sendmail command with the -bt option. Listing 11.3 shows a test of the dnsbl.foobirds.org domain.

# 11.3 Testing the dnsbl Feature

```
$ sendmail -bt Ctest-dnsbl.cf
ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
Enter <address>
> .O<client_addr>172.168.12.1
> Basic_check_relay >
rewrite: ruleset 192 input: <>
rewrite: ruleset 192 returns: OK
> .O<client_addr>192.168.72.37
> Basic_check_relay >
rewrite: ruleset 192 input: <>
rewrite: ruleset 192 returns: $# error @ $ 5 . 7 . 1
  $: "550 Mail from " * 192 . 168 . 72 . 37
    refused by blackhole site dnsbl.foobirds.org*
```

> > "D"
The client_addr variable normally contains the IP address of the system that initiated the mail connection. Because this is a -bt test, there is no mail connection, so we use the -D command to place a value in the client_addr variable. Next, the ruleset Basic_check<and> are used without any input address, which is why the focus characters do not enclose any address value. The Basic_check_relay rules does not process the input address; it processes the address found in client_addr. The first test returns OK, which shows that the local address 172.168.12.12 is an acceptable source for e-mail. Next, the address 192.168.72.37 is stored in client_addr and ruleset Basic_check_relay is running again. This the address is found in the dnsbl.foobirds.org domain, and the Basic_check_relay rules returns the error message "550 Mail from 192.168.72.37 refused by blackhole site dnsbl.foobirds.org."

The second argument for the dnsbl feature to be the error message that is displayed when mail is rejected because of the blackhole server. The default message is the