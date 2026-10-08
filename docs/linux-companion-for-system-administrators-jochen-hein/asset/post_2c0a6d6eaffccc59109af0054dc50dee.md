
## 512 CONNECTING TO THE INTERNET

In many examples (for example the ppp-on script), the chat script is passed as a command line option. This script contains user name and password. With the command ps -auxwww, each user can create an extensive process list and read the password so the pppd process is not swapped out of the memory. A better solution is to store the chat script in a file and pass the chat interpreter the option -f chatfile.

This chat script is structured similarly to UUCP. A string that comes from the modem alternates with a string to be sent to the modem. The first string to be received must be empty; further empty strings may follow. After the test stage, you should not specify the chat script in the command line of the pppd, but store it in a separate file. In Listing 23.2, but reasons of space and simplicity of presentation, this is not shown here.

```
pppd connect -chat "*AT0DT551212 \
CONNECT \
login: ppp \
word:password \
/dev/ttyUSB1 38400 debug crtscts modem \
defaultroute 192.168.99.2
```
Listing 23.2 Establishment of a PPP connection.

On my system, a normal shell script is started as a connect script instead of a chat script. This attempts a CONNECT for the different numbers of my ISP. If it succeeds, the script is terminated with 0; otherwise an error is returned to the pppd. This script is shown in Listing 23.3, whereas Listing 23.4 shows an example for a called chat script.

The messages of the pppd are managed via syslog, using the facility daemon. The file where you will find these messages is specified in the file /etc/syslog.conf. Here you will find the debug protocol which is requested by means of the parameter debug. This protocol helps you trace configuration problems; in addition, start and end of the connections are stored.

After successful establishment of a connection, the pppd program starts the script /etc/ppp/ip-up. As parameters, this script is passed the name of the network interface, the modem device, the speed of the connection, plus the personal and the remote IP address. Here, for example, mail can be automatically fetched by means of fetchmail. On my system, mail and news are exchanged via UUCP, so uucp is started via a TCP connection. Similar scripts exist for terminating a connection (/etc/ppp/ipx-up and /etc/ppp/ipx-down) and for other protocols.

## POINT-TO-POINT PROTOCOL (PPP) 513

```bash
#!/bin/sh
# number of attempts
MAXTRIES=3
host=`basename $0`
# how we were called

# repeat until number of attempts is reached
for i in `seq 1 $MAXTRIES` ; do
    # one chat script for each phone number
    for j in /etc/ppp/chat/$host-*; do
        chat FLAGS -f $j # and dial in
        rc=$?
        if [ $rc -eq 0 ]; then # successful?
            exit 0 # yes, then get out of here
        fi
    done
done
# # numbers tried without success
```
**23.3** A chat script with retries and several numbers.

```
TIMEOUT 5
ABORT "NO CARRIER"
ABORT BUSY
ABORT "NO DIALTONE"
ABORT ERROR
" ATZ
OK ATDTphone_number
CONNECT ""
name: username
word: password
Your IP: "\d\d\d"
```
**23.4** A chat script as an input file for chat.

Extensive documentation on PPP can be found in the man pages of pppd(8), chat(8), the PPP HowTo of the Linux Documentation Project, and the README files included in the ppp package.

### 23.1.3 Termination of a connection

To terminate a PPP connection, you must send the pppd SIGINT signal with a kill command. The PPP drivers will then shut down the connection in an orderly fashion, and the modem hangs up. You can find the process ID of the PPP daemon in the file /var/run/pppN.pid where N stands for the number of the PPP device.

### 23.1.4 Authentication

As a rule, you must identify yourself to your ISP with your user ID and password before the PPP drivers are started. the caller cannot be sure that the counterpart is indeed the ISP. Authentication in the opposite direction is seldom used (this also applies to everyday life). Thus, everybody assumes that cash machine behaves correctly, but there is no guarantee of this. If someone has set up a cache machine, it is only after entering your PIN that you notice that the machine does not distribute cash but has only been used to get hold of your PIN.

If auth is present in the option file, a PPP link can be established after authentication of the partner. Two methods can be implemented, the Cryptographic Handshake Authentication Protocol (CHAP) and the Password Authentication Protocol (PAP). If at all possible, you should use CHAP, although PAP will do.

### Cryptographic Handshake Authentication Protocol (CHAP)

The Cryptographic Handshake Authentication Protocol is based on the exchange of a 'challenge' that is encrypted with secret. Each partner, no matter whether calling or called, can request authentication. By means of options, you can insist on CHAP being used, or you can allow PAP. When partners need to authenticate themselves, they select the appropriate phrase from the file /etc/ppp/chap-secrets. Both partners need to know both phrases to be able to identify each other. Some ISDN routers support configuration of only one phrase; you can obtain more information from your provider or network administrator.

If the computer establishes a PPP link and CHAP is used for authentication, the secrets file must be structured as in Listing 23.4.

| remote secret | IP address |
| :--- | :--- |
| local "Hey, what's the password?" | 192.168.1.55 |
| local "Ken sent me" | 192.168.1.51 |
Listing 23.5 The file /etc/ppp/chap-secrets.

In CHAP, a 'challenge' is sent which is encrypted by the 'secret'. The secret is never transferred via the link. If the partner's answer is identical to the locally calculated result, the authentication was successful. The IP address field can be used to activate the connection with specific addresses.

## AUTOMATIC CONNECTION WITH dial 515

### Password Authentication Protocol

If authentication with CHAP is not possible, you should at least use Password Authentication Protocol (PAP). In this file, both the personal and the remote passwords are stored. The entry in Listing 23.6 is used for logging in. If the computer identifies itself by means of PAP, the second line is used for verification. Please note that some systems only have one password or secret for each communication. In this case, the password is the same for both directions.

With PAP, the password is transferred via the link. At the remote system it may be checked against the pap-secrets file or the system file (/etc/passwd) by the means of function. Since CHAP uses a different encryption algorithm PAP is not possible with.

| account remote | password | IP address |
| :--- | :--- | :--- |
| local "kwnk" | 10.10.10.2 |
| local "auemf" | 10.10.10.1 |
Listing 23.6 The file /etc/ppp/pap-secrets.

| Additional Information and Sources |
| :--- |
| Man page: pppd(8) |
| HowTo: PPP-HowTo |
| Newsgroup: comp.protocol |
| ftp server: sunsite.unc.edu |
| ftp path: /pub/Linux/system/serial |
| File name: ppp-2of.tar.gz |
| Size: about 210 Kbytes |

### 23.2 Automatic connection with dial

The procedures described up to now require the connection to be manually established and terminated by the user. This is not very efficient and it may lead to 'forgetting' an open connection which goes on accruing charges. It is much more useful if the connection is dynamically established when needed, without the user having to intervene. If the connection is not used for a certain time, it can also be automatically terminated. Since establishing and terminating connections are initiated from a root process, the pppd program in this case does not need to be setuid.

## 516 CONNECTING TO THE INTERNET

With the previously presented programs, this is not possible; you will need to use the dial program by Eric Schenk (schenk@cs.toronto.edu). dial uses a proxy interface (this must be a SLIP interface) to which all requests are redirected. If a program wants to access a remote computer, then it is recognized by dial. The connection with the provider is established in the background, and the packets are forwarded to the true PPP or SLIP interface. Thus, precondition for the use of dial is a kernel that contains both SLIP and PPP.

The dial program is configured by means of the files /etc/dial.defs and /etc/dial.conf. In the file dial.defs, symbolic names are defined for individual fields of the IP packets. They can be used in the file dial.conf to store rules for individual protocols. On the basis of these rules, the decision is made when a connection must be established and when it can be closed again. The file /etc/dial.conf is extensively commented and provided with workable default settings for nearly all protocols.

The man page contains all options and various examples for calling of dial. In addition, the distribution includes the FAQ.

| Additional Information and Sources |
| :--- |
| ftp server: sunsite.unc.edu |
| ftp path: /pub/Linux/system/Network/serial |
| File name: dial-0.13.tar.gz |
| Home page: http://www.cs.toronto.edu/~schenk/dial.html |
| Mailing list: linux-dial@vger.rutgers.edu subscribe linux-dial-to maydormomo@vger.rutgers.edu |

### 23.3 ISDN instead of a modem

In recent times, digital ISDN connections gained a growing share of the international telecommunications market, replacing traditional analogue connections. For computer users, ISDN has the advantage that up to 64 kbits per second can be transmitted in each direction. All you need is an ISDN line in your home or office and an ISDN card in your PC.

Unlike the use of a modem, the data is directly transmitted digitally and does not need to be modulated onto a carrier signal. Furthermore, ISDN connections are usually stable and have a constant speed. If the transmission rate of one ISDN channel is not sufficient, channel bundling is possible in some cases. Furthermore, establishing connections is extremely fast, so 'dial-on-demand' can easily be implemented without causing noticeable delays for the user.
