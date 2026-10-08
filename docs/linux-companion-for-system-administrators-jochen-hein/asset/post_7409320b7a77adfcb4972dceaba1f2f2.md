
## 15.4.1 Interactive DNS requests with nslookup

With the nslookup program, DNS requests can be made in two modes: interactive and non-interactive. In interactive mode, different requests can be made one after the other. In non-interactive mode, only the required information is displayed and the program terminated.

Additional options can be specified with a leading minus sign (-) either before the host name or before the address. Furthermore, default values can be stored in the file ~/.nslookuprc. An example for a non-interactive call of nslookup can be found in Listing 15.4.

The interactive mode is used if either no parameter is specified or a name server (name or IP address) is specified after a minus sign (-). Subsequently, requests can be started by entering a host name or an IP address. The command set type=any can be used to request all information on a computer. An example can be found in Listing 15.5. More detailed information on nslookup and a list of all possible request options can be found in the man page for nslookup(1).

```
(Linux): > nslookup ftp
server: carrot.example.org
Address: 192.168.3.150

name: pea.example.org
Address: 192.168.3.150
Aliases: ftp.example.org
```

Listing 15.4 nslookup in non-interactive mode.

```
(Linux):> nslookup
Default server: carrot.example.org
Address: 192.168.3.150

> ftp
server: carrot.example.org
Address: 192.168.3.150

name: pea.example.org
Address: 192.168.3.155
Aliases: ftp.veggies.example.org

> set type=any
> ftp
server: carrot.veggies.example.org
Address: 192.168.3.350

ftp.veggies.example.org canonical name = pea.veggies.example.org
veggies.example.org nameserver = carrot.veggies.example.org
pea.example.org internet address = 192.168.3.155
> exit
```

Listing 15.5 nslookup in interactive mode.

The nslookup program can also be used to carry out a reverse lookup, that is, a request for the name belonging to a specific IP address. In this case, you simply specify the IP address instead of the host name.

The nslookup program can interrogate different name servers and analyse the sent and received packets. Since this program is also available under other systems, such as Windows NT, it is very widely used for testing name servers.

## 15.4.2 Name server requests with host

The host program also allows you to analyse data stored in a name server. Here, a useful feature is that the data can be output in the format required for name database entries (option -v). With the option -t, the required entries can be selected (for example ns, cname, soa, hinfo, mx, and any or * for all entries). The meaning of the entries is explained in more detail in Chapter 21.

The option -a is a short form for any. A more detailed description of all entries can be found in the man page host(1) and in the ‘Bind Operators Guide' is supplied together with the sources of bind. Listing 15.6 shows some of the use of host.

```
(Linux)> host pea
pea.example.org has address 192.168.3.155
(Linux)> host -v pea
Trying domain "example.org"
rcode = 0 (Success), answer:
pea.example.org A 86400 IN
For authoritative answers, see:
example.org 86400 IN NS carrot.org
Additional information:
carrot.example.org 86400 A 192.168.3.150
(Linux)> host -m pea
Trying domain "example.org"
rcode = 0 (Success), answer:
pea.example.org 86400 IN A 192.168.3.155
pea.example.org 86400 IN HINFO IBM-PC/AT UNIX-PC
pea.example.org 86400 IN TXT "Test with text"
For authoritative answers, see:
example.org 86400 IN NS carrot.org
```

Listing 15.6 Name server requests with host.

## 15.4.3 Name server requests with dig

Another tool for the analysis of a name server is dig (Domain Information Groper). This program can be used interactively and in many mode. Many TCP/IP packages contain only this program and not nslookup host.

The options and functions of dig are extensively described in the manual page. Please note that for a 'reverse lookup' you must specify the option -x in addition to the IP address.

## 15.5 Reliability of name servers

Until now, the Internet protocols have been developed and implemented with a view to implementation techniques and functionality. This was no problem so long as only a few and reliable users participated in the Internet. In the past years, the number of Internet computers and users has grown substantially.
