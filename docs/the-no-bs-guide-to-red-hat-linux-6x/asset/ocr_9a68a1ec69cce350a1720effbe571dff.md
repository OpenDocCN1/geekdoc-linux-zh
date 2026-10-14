Refer to Chapter 11, “Compression, Encoding, and Encryption,” for more information on handling compressed files.

# USING TELNET

Telnet is a tool that lets you log in to other computers on the Internet. Why would you want to do that? Simple: to access the interesting stuff on those other computers, such as databases, games, card catalogs, and information services. If you have a shell account with your ISP, you might want to telnet there from your Linux system and check your email with Pine.

Telnet is strictly text-based—you can’t point or click on anything. Whether you telnet from a command line or from a GUI, your Telnet session will look pretty much the same, and all your navigation in a Telnet session is via the keyboard. To start a text-based Telnet client from your Linux command line, enter the telnet command followed by a site name (and, sometimes, a port number), like this:

```
telnet cybersurf.com
```

This is a fictitious example that shows how you might log in to a shell account on your ISP’s system. Here’s a real example that will connect you to the Ham Radio Call Book database at the University of Buffalo (commands you enter are shown in boldface):

```
telnet electra.cs.buffalo.edu 2000
```

```
Connected to electra.cs.buffalo.edu.
Callbook v1.3 -- Type 'help' for help
>> help
Available commands:
    call [filters] callsign    - lookup callsign
    city [filters] city        - lookup city
    name [filters] surname     - lookup last name
    quit                       - exit the server
    zip [filters] zipcode      - lookup zip code
> city Tillson
Call-Sign: WA2TNW            Class: GENERAL
Real Name: DONALD G WOOD     Birthday: OCT 31, 1919
Mailing Address: BOX 873 ROSE AVE, TILLSON, NY 12486
Valid From: DEC 29, 1987     To: DEC 29, 1997
>> quit
```