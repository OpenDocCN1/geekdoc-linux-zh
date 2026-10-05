# GOING INTERNET WITH LINUX

Let us now explain the terms occurring in the above list: the table starts with the phone number. This is the number you must dial with your modem in order to contact the Internet provider.

# Email address

The email address specifies where other Internet users can send email for you to read either interactively or via PPP/SLIP. Usually, the mail address of your name or an abbreviation or a composite word. The domain name of the Internet provider (in the above example, `provider.de`).

# User name and password

User name and password are required to establish a PPP or SLIP connection with the provider. As a rule, the user is the same as the name in the email address, but this not necessarily be the case.

Depending on the provider, PPP utilization is recognized automatically, or by you to start PPP after login via an explicit command, such as `ppp`. Some providers differentiate between PPP and interactive utilization using different names and passwords. If you have established the connection by means of a terminal emulator, only strange characters are displayed forthwith. In order to make your computer react properly to this, you must now quit the terminal emulator and take over the connection with either slattach (SLIP) or `pppd` (PPP). Details follow further below.

# IP number

As soon as the PPP/SLIP connection is established, you are a member of the Internet! However, in the above list you will look for the IP number under which you can be reached on the Internet. The reason: Most providers manage a pool of IP addresses and dynamically assign these at each login. In other words, you receive a different IP address, namely the first of your provider's numbers that happens to be free.

> CAUTION This connection is bidirectional - that is, you have access to external computers, but Internet users theoretically have access to your computer too. Now is the time for you to protect all user names on your computer with passwords, if you have not already done so in the first place!

Further data may be specified for mutual identification only for PPP (and not for SLIP). Besides the password, this mutual identification is an additional safety mechanism which works in both directions (not only you, but also the provider must transmit an identification number before a `TCP/IP` connection is established).

# Name server

The above list also contains an IP number which refers to a server of your Internet provider. This server determines the IP numbers corresponding to Internet addresses used by you (such as `www.addison-wesley.de` in the Web browser). Thus, the main name server (DNS) is of great importance for the proper functioning of your Internet connection.