
In this configuration, elmo's account is the most restrictive because it only allows logging on to the server machine sesame, and only accepts the IP address 192.168.1.101. The bert and ernie accounts are both more flexible; they'll accept any remote server and any IP addresses.

Chances are you only need a single-line pap-secrets/chap-secrets file, excluding comments (lines that begin with a pound sign [#]). When the system has established a PPP link, any user can use it. So if Bert connects to his ISP, Elmo and Ernie can use that link. If these accounts are on different ISPs, these users may experience difficulties accessing some ISP services, such as email or Usenet news, when the machine is connected to a foreign ISP. This is because many ISPs check the source of incoming requests for services such as these, and refuse such requests if they come from another ISP. Web browsing, Telnet, FTP downloads, and similar functions work fine for all users, though.

## Creating PPP Scripts

Red Hat Linux 6.0 includes a few basic PPP support files, including pppd, the PPP daemon that's used both for initiating PPP sessions and listening for them if you want your computer to function as a dial-in PPP server. If you want to actually use these features, though, you've got to link them together in some way. One way to do this is to write a short script to do the job. In fact, you need three scripts: two to initiate the PPP session and one to terminate it. Because you'll be using scripts if you want to configure a dial-on-demand setup, as described in the section "Setting Up Dial-on-Demand for Automatic Connections" later in this chapter, I present more basic scripts here. You might prefer to use a more GUI-oriented approach, and there are several GUI PPP dialers available, so I present instructions on using one in the section "Using a GUI PPP Dialer" later in this chapter.

## NOTE

> You might need to modify these scripts for your system. At the very least, you need to insert your own username and ISP phone number in the ppp-on script. You might also need to change the other scripts to accommodate your hardware or software needs, or the needs of your ISP. Some information on debugging PPP connections appears in the "PPP Problem-Solving" section later in this chapter.

## Creating the ppp-on Script

First, here's a basic ppp-on script. You can type this in, save it in /usr/local/bin or some other convenient location, and give it execute permission. There's also a version of this file on the CD-ROM that accompanies this book, in the sams-extras/ppp directory. Without further ado, then, here's the script:

## Creating the ppp-on-dialer Script

Just as you created the ppp-on script, you must create the ppp-on-dialer script. Either it must go in the /etc/ppp directory or you must modify the reference to this script in the ppp-on script. Here’s a sample of ppp-on-dialer (again, you can find this file on the CD-ROM that accompanies this book):

```
#!/bin/sh
#
# This is part 2 of the ppp-on script. It will perform the
# connection protocol for the desired connection.
#
exec /usr/sbin/chat -v
TIMEOUT 3
ABORT '\nBUSY\r'
ABORT '\nNO ANSWER\r'
ABORT '\nRINGING\r\n\r\nRINGING\r'
'' 'AT'
'OK' 'ATZ'
TIMEOUT 40
'OK' ATDT$TELEPHONE
'CONNECT'
```

This script simply runs /usr/sbin/chat, which is a utility to transfer data to the serial port in response to certain strings. Aside from keywords such as TIMEOUT and ABORT, the left column contains expect strings, which are what the program expects to see from the modem, and the right column contains send strings, which the program sends in response. Some comments on the specifics are in order here:

- The backslash (\ ) characters at the ends of most lines are line continuation characters; many Linux programs, including shells, recognize these as signaling the extension of one line on the next physical line. They’re used here because chat expects its input on a single line, but a multiline format is much easier for humans to understand.
- In response to OK, chat is to send ATZ. This is the modem initialization code, and in this case resets the modem to its defaults. You can change this string to anything else you like—say, to reduce the modem’s volume or alter its dial speed. Consult your modem’s documentation for details, or copy an initialization string that you like from another program. Different modems use different command codes, though, so don’t copy a string from a system that uses a modem that’s a different model than yours.
- The TIMEOUT value of 40 should be adequate for most situations, but if your ISP takes a long time to answer the phone, you might need to increase the TIMEOUT value.
