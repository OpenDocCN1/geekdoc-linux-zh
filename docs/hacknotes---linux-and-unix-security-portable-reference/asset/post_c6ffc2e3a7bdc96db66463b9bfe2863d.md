
# The Plug-In

This section describes how to use Nessus to detect the presence of the file /src/password.inc on a web server. First, we must write a NASL script to do this. The script will serve as a Nessus “plug-in.” Here is what such a script will look like:

```
if(description)
  script_id(99999);
  script_version("$Revision: 1.0 $");
  script_name(english: "Checks for /src/password.inc");
  desc["ENGLISH"] = "/src/password.inc is usually installed by XYZ algorithm and contains user password information in clear text."
```

Solution: Configure your web-browser to not serve .inc files.

Risk factor: High;

```
script_description(english:desc["english"]);
  script_summary(english:"Checks for the existence of /src/password.inc");
  script_category(ACT_GATHER_INFO);
  script_copyright(english:"This script is Copyright (C)2003 Nitesh Dhanjani");
  script_family(english:"CGI abuses");
  script_require_ports("Services/www", 80);
  exit(0);
  include("http_func.inc");
  port = 80;
```

```
if(get_port_state(port))
{
  hget = http_get(item:"/src/passwd.inc", port:port);

  mysoc = http_open_socket(port);

  if(!mysoc) exit(0);

  send(socket:mysoc, data:hget);

  myrec = http_recv(socket:mysoc);

  http_close_socket(mysoc);

  if (!("404") <> myrec)
{
  security_hole(port);
}
}
```

The description variable's value is set to 1 when the script is run by Nessus to extract summary information about the plug-in. Thereof, we define various plug-in description variable values when the value of description is true, nonzero.
The script_id function sets a unique ID for the plug-in. Every plug-in's value must be unique. In our case, we can set it to a high number such as 9999 to ensure a distinct value. The script_version function displays version information about the plug-in. It is a good idea to update this to reflect the latest version of the plug-in. The script_description function sets the description of the plug-in that is displayed by the Nessus client when the plug-in is queried by a user. Similarly, the script_summary function is used to set a summary of the plug-in.
The script_category function sets the plug-in's category as required by Nessus. In our case, we have set it to ACT_GATHER_INFO because the plug-in gathers information on a remote service; it checks for the existence of the file /src/passwd.inc on a web server. The script_copyright function is used to set author copyright information.
Nessus categorizes plug-ins into different “families” to help sort the vulnerabilities performed. We have set it to “CGI abuses” to indicate an abuse of a CGI-based web application. Visit http://cgi.nessus.org/plugins/dump.php?viewby=family to check out a list of publicly available plug-ins that have been categorized by family.
Nessus can be configured to optimize tests by selecting the appropriate private check in the Scan Option of the GUI client. When this option is enabled, Nessus scans for vulnerabilities that are related to the applications running on the open ports of the target machine. script_require_ports function can be used to set the port that relates to the vulnerability on the remote machine, which in our case is set to www (HTTP).

The functions just described set various values for the plug-in. Plug-ins descriptions can be viewed by double-clicking the appropriate plug-name in the list of plug-ins displayed in the Plugins tab of the Nessus GUI client. A screenshot of this appears as Figure 10-1.

The http_func.inc file contains a list of useful HTTP functions for our convenience. We make use functions defined in the file, we have included in this file using the include function.

The get_port_state function is used to check the status of a particular port on the target host. In our case, we check for port 80. If this port is closed, there is no point in going further, and therefore we call exit(0).

In order to check for the presence of the /src/passwd.inc file on a web server, the HTTP request to the web server upon connect must be formatted like this:

```
GET /src/passwd.inc HTTP/1.0
```

![](img/17cb132e62949dc7f5e0eadf90c71f51_219_0.png)

Figure 10-1. Plug-in description as displayed by the Nessus GUI client

The preceding GET request can be created by using the http_get function. This request can then be used as a parameter to the send function, which sends the request to the target host on the socket opened by the http_open_sock function. Resultant data from the web server is read using the http_recv function, and its contents are stored in the myrec variable. After this is done, the socket descriptor is closed using http_close_socket. The contents of myrec are then examined for the substring 404, which would be present if the file did not exist on the web server. Then use the <operator, which checks for a substring in a given string variable. If 404 is not found in the returned data from the web server, then it is probable that this file exists, and this fact is indicated to Nessus by calling the security_hole function.
Please see http://www.nessus.org/doc/nasl2_reference.pdf for the latest NASL reference manual.

# Running the Plug-in

Make sure the preceding script is placed in Nessus's plugins directory. The filename of the script must end with the extension "nasl." Run the Nessus GUI and select the Plugins tab. Make sure CGI Abuses are selected. Highlight CGI Abuses and make sure the plug-in with the name "Checks for /src/password.inc" is enabled. If you have trouble finding the plug-in, click the Filter button and perform a search for the ID of 99999.
To get a positive result from our plug-in, you must have a local web server configured to serve the /src/passwd.inc file. If you have an Apache web server running, simply:

```
mkdir /www/html
touch /src/passwd
```

Input the IP address or name of target in Selection tab and click Start. If everything goes well, Nessus will detect vulnerability, as shown in Figure 10-2.

# Chapter 10: Nessus Attack Scripting Language (NASL) 65

![](img/17cb132e62949dc7f5e0eadf90c71f51_219_0.png)

**Figure 10-2.** Nessus report indicating the presence of /src/password

# 166 Part III: Special Topics

# Chapter 11

## Wireless Hacking

IN THIS CHAPTER:
- Introduction to WEP
- Antennas
- Popular Tools
- Securing Wireless Networks

# 170 Part III: Special Topics

Wireless networks are a breeze to set up and a boon for those who abhor having to be tied to Ethernet cables. They are also a nightmare from a security point view due to the vulnerability of the Wired Equivalent Privacy (WEP) protocol used in 802.11 standard. Because of freely available open tools such as Airodump and Kismet, it is possible for anyone with a wireless network card and a laptop to intrude into wireless networks. Individuals have been known to go around town while looking for corporations whose wireless network ranges beyond their office space to reach accessible spots such as parking lots, an activity termed "war driving." Unfortunately, many wireless network administrators do not realize this and are unaware of their susceptibility to these intruders. This chapter describes the tools and techniques used by intruders to obtain access into wireless networks, and it includes suggestions on how to better secure them.

# INTRODUCTION TO WEP

Since WEP is based on a symmetric shared-key system, it uses the same key to encrypt and decrypt data. The keys ($k$), which are either 128 bits or 64 bits long, consist of 24-bit Initialization Vector (IV). A WEP payload is constructed as follows:

- Message $M$ is concatenated with its own CRC-32 checksum: $c(M)$:

| $M$ | $c(M)$ |

- The IV is applied before the secret key and passed through the RC4 stream cipher algorithm:

| $RC4(IV,k)$ |

- The results of steps 1 and 2 are XOR'd (eXclusive OR) to produce the cipher text. The $IV$ is then concatenated with the cipher text to produce the WEP payload:

| $IV$ | Cipher-text = $((M),c(M))$ XOR $(RC4(IV,k))$ |

As is evident from the preceding steps, the WEP frame contains the IV in clear text. Many wireless cards pick their IVs at random, while others start from 0 and increment them sequentially. Since the IV is only 24 bits long, a wireless card or access point will reuse one every few hours.

# SUMMARY

This chapter demonstrates the ease of writing plug-ins for Nessus. First, an example vulnerability was presented. Next, the creation of NASL script from scratch was discussed. Instructions on how to incorporate NASL script into Nessus were also provided. Quite often, large organizations use vulnerability detection may be vital to security posture.
